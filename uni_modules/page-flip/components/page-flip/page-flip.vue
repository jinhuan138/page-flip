<template>
    <view class="book" @click="handleClick">
        <view v-for="(item, index) in bookPapers" class="list-page" :class="{ flipped: page > index }" :key="index"
            :style="[pageStyle(index)]">
            <image :src="item.frontPage" class="front-page" lazy-load />
            <image :src="item.backPage || item.frontPage" class="back-page" lazy-load />
        </view>
    </view>
</template>

<script>
export default {
    name: "page-flip",
    emit: ["pageChange"],
    props: {
        papers: {
            type: Array,
            default() {
                return [];
            },
        },
    },
    data() {
        return {
            page: 0,
        };
    },
    watch: {
        page(val) {
            this.$emit("pageChange", val * 2);
        },
    },
    computed: {
        bookPapers() {
            const bookPapers = [];
            for (let i = 0; i < this.papers.length; i += 2) {
                const onePage = {
                    frontPage: this.papers[i],
                };
                if (this.papers[i + 1]) {
                    onePage.backPage = this.papers[i + 1];
                }
                bookPapers.push(onePage);
            }
            return bookPapers;
        },
    },
    methods: {
        next() {
            if (this.page < this.bookPapers.length) {
                this.page++;
            }
        },
        prev() {
            if (this.page > 0) {
                this.page--;
            }
        },
        pageStyle(index) {
            if (this.page > index) {
                return {
                    transform: `translateZ(${index * 0.1}px) rotateY(-180deg) translateX(4%)`,
                };
            } else {
                return {
                    transform: `translateZ(${(this.bookPapers.length - index) * 0.1}px)`,
                };
            }
        },
        handleClick(e) {
            const { x } = e.detail;
            const query = uni.createSelectorQuery().in(this);
            query
                .select(".book")
                .boundingClientRect((data) => {
                    if (x > data.width / 2) {
                        this.next();
                    } else {
                        this.prev();
                    }
                })
                .exec();
        },
    },
};
</script>

<style scoped lang="scss">
.book {
    perspective: 3000px;
    transform-style: preserve-3d;
    position: relative;
    height: 100%;
    width: 100%;
    --animation-duration: 1s;

    .list-page {
        height: 80%;
        width: 49%;
        position: absolute;
        right: 0;
        top: 0;
        transform-origin: left;
        transform-style: preserve-3d;
        transition: transform var(--animation-duration) ease-in-out;

        .front-page,
        .back-page {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            backface-visibility: hidden; //隐藏旋转元素的背面
        }

        .back-page {
            transform: rotateY(180deg);
        }

        &.flipped {
            transform: rotateY(-180deg);
        }
    }
}
</style>
