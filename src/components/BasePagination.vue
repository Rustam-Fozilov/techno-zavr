<template>
    <ul class="catalog__pagination pagination">
        <li class="pagination__item">
            <a href="#" class="pagination__link pagination__link--arrow" :class="{'pagination__link--disabled' : this.page === 1}" @click.prevent="paginatePrev" aria-label="Предыдущая страница">
                <svg width="8" height="14" fill="currentColor">
                <use xlink:href="#icon-arrow-left"></use>
                </svg>
            </a>
        </li>
        <li class="pagination__item" v-for="pageNumber in pages" :key="pageNumber">
            <a href="#" class="pagination__link" :class="{'pagination__link--current' : pageNumber === this.page}" @click.prevent="paginate(pageNumber)">
                {{ pageNumber }}
            </a>
        </li>
        <li class="pagination__item">
            <a href="#" class="pagination__link pagination__link--arrow" :class="{'pagination__link--disabled' : this.page === this.pages}" @click.prevent="paginateNext()" aria-label="Следующая страница">
                <svg width="8" height="14" fill="currentColor">
                <use xlink:href="#icon-arrow-right"></use>
                </svg>
            </a>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'BasePagination',
    props: ['page', 'count', 'perPage'],

    computed: {
        pages() {
            return Math.ceil(this.count / this.perPage);
        }
    },

    methods: {
        paginate(page) {
            this.$emit('paginate', page);
        },
        paginateNext() {
            this.$emit('paginate', this.page + 1);
            if(this.page === this.pages) {
                this.$emit('paginate', this.page);
            }
        },
        paginatePrev() {
            this.$emit('paginate', this.page - 1);
            if(this.page === 1) {
                this.$emit('paginate', this.page);
            }
        }
    }
}
</script>