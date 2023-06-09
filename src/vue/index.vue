<template>
    <div
        class="vue-pithy-pagination"
        @click="showPage = false"
    >
        <div class="pageTotal">
            共<span>{{ allCount }}</span>条
        </div>
        <div class="pageContent">
            <button
                class="firstPage blue-button"
                :disabled="currentPage === 1"
                :class="[currentPage === 1 ? 'disableStyle' : '']"
                @click="firstPage"
            >
                首页
            </button>
            <button
                class="prevPage"
                :disabled="currentPage === 1"
                :class="[currentPage === 1 ? 'disableStyle' : '']"
                @click="prevPage"
            >
                <i class="iconfont icon-arrow-left" />
            </button>
            <button class="showPage blue-button">
                {{ currentPage }}
            </button>
            <button
                class="nextPage"
                :disabled="currentPage === Math.ceil(allCount / pageCount)"
                :class="[currentPage === Math.ceil(allCount / pageCount) ? 'disableStyle' : '']"
                @click="nextPage"
            >
                <i class="iconfont icon-arrow-right" />
            </button>
            <button
                class="lastPage blue-button"
                :disabled="currentPage === Math.ceil(allCount / pageCount)"
                :class="[currentPage === Math.ceil(allCount / pageCount) ? 'disableStyle' : '']"
                @click="lastPage"
            >
                尾页
            </button>
        </div>
        <div class="selectSize">
            <div>
                <span class="numSelect">{{ pageCount }}</span> <span>条/页</span>
            </div>
            <div
                class="icona"
                @click.stop="showPageCount"
            >
                <i
                    class="iconfont"
                    :class="[showPage ? 'icon-arrow-up' : 'icon-arrow-down']"
                />
            </div>
        </div>
        <!-- <div id="test1" style="display: inline-block;margin-left: 210px;"></div> -->
        <div class="goPage">
            <span>跳至</span><input
                type="text"
                @keyup.enter="jumpPage($event)"
            ><span>页</span>
        </div>
        <ul
            v-if="showPage"
            class="pageSelectShow"
        >
            <li
                data-num="10"
                @click="choosePage(10)"
            >
                10条/页
            </li>
            <li
                data-num="20"
                @click="choosePage(20)"
            >
                20条/页
            </li>
            <li
                data-num="50"
                @click="choosePage(50)"
            >
                50条/页
            </li>
            <li
                data-num="100"
                @click="choosePage(100)"
            >
                100条/页
            </li>
        </ul>
        <div class="pageTotal">
            共<span>{{ Math.ceil(allCount / pageCount) }}</span>页
        </div>
    </div>
</template>

<script>
export default {
    name: 'VuePithyPagination',
    props: {
        allCount: {
            type: Number,
            require: true,
            default: 10
        },
        pageCount: {
            type: Number,
            require: true,
            default: 1
        }
    },
    data() {
        return {
            currentPage: 1, // 当前页
            showPage: false
        };
    },
    methods: {
        // 首页
        firstPage() {
            this.currentPage = 1;
            this.$emit('getCurrentPage', this.currentPage);
        },
        // 上一页
        prevPage() {
            this.currentPage -= 1;
            this.$emit('getCurrentPage', this.currentPage);
        },
        // 下一页
        nextPage() {
            this.currentPage += 1;
            this.$emit('getCurrentPage', this.currentPage);
        },
        // 尾页
        lastPage() {
            this.currentPage = Math.ceil(this.allCount / this.pageCount);
            this.$emit('getCurrentPage', this.currentPage);
        },
        // 显示选择跳数
        showPageCount() {
            this.showPage = true;
        },
        // 选择条数
        choosePage(pageCount) {
            this.showPage = false;
            this.$emit('choosePage', pageCount);
            this.firstPage();
        },
        // 键盘跳转
        jumpPage(e) {
            //   console.log(jumpPageCount);
            const jumpPageCount = Number(e.target.value);
            if (jumpPageCount > Math.ceil(this.allCount / this.pageCount)) {
                return;
            }
            this.currentPage = jumpPageCount;
            this.$emit('getCurrentPage', this.currentPage);
            e.target.value = '';
        }
    }
};
</script>

<style lang="scss" scoped>
@font-face {
    /* stylelint-disable-next-line */
    font-family: iconfont;
    /* Project id 3941812 */
    src: url('//at.alicdn.com/t/c/font_3941812_qaluwoj9q0c.woff2?t=1686215479016') format('woff2'),
        url('//at.alicdn.com/t/c/font_3941812_qaluwoj9q0c.woff?t=1686215479016') format('woff'),
        url('//at.alicdn.com/t/c/font_3941812_qaluwoj9q0c.ttf?t=1686215479016') format('truetype'),
        url('//at.alicdn.com/t/c/font_3941812_qaluwoj9q0c.svg?t=1686215479016#iconfont') format('svg');
}
.iconfont {
    /* stylelint-disable-next-line */
    font-family: iconfont !important;
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-style: normal;
}
.icon-arrow-down:before {
    content: '\e65e';
}
.icon-arrow-left:before {
    content: '\e65f';
}
.icon-arrow-up:before {
    content: '\e660';
}
.icon-arrow-right:before {
    content: '\e661';
}
.vue-pithy-pagination {
    position: relative;
    display: flex;
    width: 70%;
    height: 50px;
    align-items: center;
    margin-top: 200px;
    margin-left: 15%;
    .pageContent {
        display: flex;
        align-items: center;
        margin: 0 15px;
        button {
            border: none;
            margin: 0 4px;
            cursor: pointer;
            outline: none;
            &.blue-button {
                border-radius: 4px;
                background: rgb(67, 133, 255);
                color: #fff;
                font-size: 15px;
                line-height: 30px;
                text-align: center;
            }
        }
    }
    .goPage,
    .pageTotal {
        height: 30px;
        font-size: 14px;
        vertical-align: middle;
    }
    .goPage {
        display: flex;
        align-items: center;
        margin: 015px;
        span {
            color: #999;
        }
        input {
            display: inline-block;
            width: 50px;
            height: 30px;
            border: none;
            border: 1px solid #ccc;
            border-radius: 4px;
            margin: 0 5px;
            text-align: center;
        }
    }
    .pageTotal {
        left: 50px;
        color: #999;
        font-size: 15px;
        line-height: 30px;
        span {
            margin: 0 3px;
            color: #333;
        }
    }
    .selectSize {
        position: relative;
        display: flex;
        width: 100px;
        height: 30px;
        align-items: center;
        border: 1px solid #ccc;
        border-radius: 4px;
        font-size: 14px;
        line-height: 30px;
        text-align: center;
        vertical-align: middle;
        div {
            margin-left: 5px;
        }
    }
    .icona {
        position: absolute;
        right: 6px;
        display: flex;
        width: 20px;
        height: 20px;
        align-items: center;
        justify-content: center;
        cursor: pointer;
    }
    .pageSelectShow {
        position: absolute;
        top: -180px;
        left: 392px;
        width: 100px;
        height: 162px;
        padding: 0;
        border: 1px solid #ccc;
        border-radius: 3px;
        background: #fff;
        font-size: 15px;
        list-style: none;
        overflow-y: auto;
        li {
            width: 100%;
            height: 40px;
            cursor: pointer;
            line-height: 40px;
            text-align: center;
        }
    }
    .firstPage,
    .lastPage {
        width: 60px;
    }
    .showPage {
        width: 40px;
    }
    .prevPage,
    .nextPage {
        width: 50px;
        height: 30px;
        border: 1px solid #ccc;
        border-radius: 4px;
        background-position: center center;
        background-repeat: no-repeat;
        background-size: 20px 20px;
    }
    .nowtouch {
        color: #009e94;
    }
    .disableStyle {
        cursor: not-allowed;
        opacity: 0.5;
    }
}
</style>
