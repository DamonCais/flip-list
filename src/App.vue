<template>
<div id="app">
    <div class="flex">
        <button @click="flag=!flag">开关</button>
        <button @click="sort">排序</button>
    </div>
    <div class="flex">
        <div class="tabs-wrap" :class="flag?'active':''">
            <transition-group name="flip-list" class="tabs-items" tag="ul" mode="in-out">
                <li v-for="i in list" :key="i" :class="currentItem==i?'current-item':''" class="tab flip-list-item">{{i}}</li>

            </transition-group>

        </div>
        <ul class="tabs" :class="flag?'active':''">
            <li v-for="i in list" :key="i" class="item">{{i}}</li>
        </ul>
        <div class="content">
            <div class="content-wrap">
                内容
            </div>

        </div>
    </div>

</div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
    name: "Home",
    mounted() {
        this.list = [1, 4, 5, 7, 2, 3, 6, 11, 14, 15, 17, 12, 13, 16, 21, 22, 23];
    },
    data() {
        return {
            currentItem: 5,
            list: [],
            flag: true
        };
    },
    methods: {
        sort() {
            this.list = this.list.sort((a, b) => Number(a) - Number(b));
        }
    }
};
</script>

<style lang="scss">
.tabs {
    list-style: none;
    width: 50px;
    margin: 0;
    padding: 0;
    margin-right: 20px;
    transition: all 0.3s;

    &.active {
        width: 150px;
    }

    .item {
        border: 1px solid blue;
        height: 50px;
        line-height: 50px;
        min-width: 50px;
        opacity: 0;
    }
}

.flex {
    display: flex;
    position: relative;
    max-height: calc(100vh - 50px);
    overflow: hidden;

    .content {
        flex: 1;
        overflow-y: auto;

        .content-wrap {
            background: greenyellow;
            height: calc(120vh);
        }
    }
}

.tabs-wrap {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    width: 150px;
    overflow-x: hidden;
    overflow-y: auto;
    z-index: 2;

    &::-webkit-scrollbar {
        /*滚动条整体样式*/
        width: 10px;
        /*高宽分别对应横竖滚动条的尺寸*/
    }

    &::-webkit-scrollbar-thumb {
        background-color: rgba(0, 0, 0, 0);
    }

    &.active {
        &::-webkit-scrollbar-thumb {
            background-color: rgba(0, 0, 0, 0.4);
        }
    }
}

.tabs-items {
    list-style: none;
    width: 150px;
    margin: 0;
    padding: 0;
    margin-right: 20px;
    transition: all 0.3s;
    height: auto;

    .tab {
        width: 50px;
        border: 1px solid blue;
        height: 50px;
        line-height: 50px;
        min-width: 50px;
        background: hotpink;

        transition: all 0.3s;

        &:hover {
            width: 150px;
        }
    }
}

.active {
    .tab {
        width: 150px;
    }
}

.current-item {
    background: blue;
}

.flip-list-enter-active,
.flip-list-leave-active {
    transition: all 0.5s;
}

.flip-list-move {
    transition: all 0.5s;
}

.flip-list-enter,
.flip-list-leave-to {
    opacity: 0;
    transform: translateX(50px);
}

/**
 * 要让删除的元素先脱离文档流，旁边的元素才能过渡过来
 */
.flip-list-leave-active {
    position: absolute;
}
</style>
