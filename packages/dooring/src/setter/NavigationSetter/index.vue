<!--
 * @Description: 文本控件
 * @Autor: WangYuan1
 * @Date: 2022-10-18 10:45:43
 * @LastEditors: WangYuan
 * @LastEditTime: 2024-09-24 10:54:53
-->
<template>
  <div>
    <!-- <div>{{ model }}</div> -->
    <SetterItem :title="props?.schema?.title">
      <div class="flex items-center cursor-pointer text-12">
        <div
          class="flex items-center c-theme bg-#3662ec20 border-1 border-solid border-#3662ec rd-4 p-6"
          v-if="model.id"
          @click="handleOpen"
        >
          <span>{{ model.name }}</span>
          <div class="flex-center h-full w-18 text-14" @click.stop="model = {}">
            x
          </div>
        </div>
        <div v-else class="c-theme" @click="handleOpen">选择要跳转页面</div>
      </div>
    </SetterItem>

    <Dialog ref="HotSpotRef" v-model="model" @submit="handleSubmit" />
  </div>
</template>

<script setup lang="ts">
import { ref, provide, computed } from "vue";
import { cloneDeep } from "@design/utils";
import { useVModel } from "@vueuse/core";
import Dialog from "./Dialog";
import SetterItem from "@/components/SetterItem/index.vue";

const props = defineProps({
  modelValue: {
    type: Object,
    default: () => {
      return {};
    },
  },
  schema: {
    type: Object,
    default: () => {},
  },
});

// v-model 配置
const emit = defineEmits(["update:modelValue"]);
const model = useVModel(props, "modelValue", emit);
const HotSpotRef = ref<any>();
// provide("project", props.project);

// const label = computed(() => {
//   console.log("model.value.type", model.value.type);
//   // if (model.value.type == "wechat") {
//   return [...props.project.pageList, { name: "我的", id: "my" }].find(
//     (item) => item.id == model.value.value
//   )?.name;
//   // }

//   return "";
// });

function handleOpen() {
  HotSpotRef.value.open(cloneDeep(model.value));
}

function handleSubmit(target) {
  console.log("target", target);
  model.value = target;
}
</script>

<style lang="scss" scoped>
.setter {
  padding: 0 15px;

  .setter-title {
    padding: 20px 0;
    font-size: 14px;
    color: #333;
  }

  .setter-description {
    margin-bottom: 15px;
    font-size: 12px;
    color: #bbb;
  }

  .setter-image {
    height: 164px;
    background: #f9f9f9;
    border-radius: 3px 3px 3px 3px;
    font-size: 12px;
    color: #bbb;
    text-align: center;
    line-height: 164px;
  }

  .setter-upload {
    display: flex;
    align-items: center;
    height: 96px;
    background: #f9f9f9;
    border-radius: 3px;
    width: 100%;
    margin-top: 20px;
    padding: 0 20px;

    .setter-upload-add {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 64px;
      height: 64px;
      margin-left: 20px;
      background: #fff;
      border-radius: 4px;
      border: 1px solid #eee;
      font-size: 40px;
      color: #d2d2d2;
      cursor: pointer;
    }
  }

  .setter-button {
    width: 100%;
    height: 36px;
    border-radius: 3px;
    opacity: 1;
    border: 1px solid #eee;
    color: #666;
    font-size: 12px;
    text-align: center;
    line-height: 36px;
    margin-top: 20px;
    cursor: pointer;
  }
}
</style>
