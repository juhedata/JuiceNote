<template>
  <header>
    <Toast></Toast>

    <div class="flex h-full justify-end gap-4" :class="{ 'mr-40': isWindows }" v-if="!route.name?.toString().startsWith('setting')">
      <Toolbar :editor="editor" :current="current" v-if="editor && editable"></Toolbar>
      <div class="flex flex-row items-center justify-end gap-0 pr-4">
        <BtnOfficialLink></BtnOfficialLink>
        <Add :node="current" :show-text="false" class="operators" v-if="!isShop"></Add>
        <Home class="operators"></Home>
        <Edit :showText="false" class="operators" v-if="current.isPage && !isShop"></Edit>
        <More :node="current" class="operators"></More>
        <Setting :show-text="true" class="operators" v-if="isSetting"></Setting>
      </div>
    </div>

    <div class="flex h-full justify-end gap-4" :class="{ 'mr-40': isWindows }" v-if="route.name?.toString().startsWith('setting')">
        <div class="flex flex-row items-center justify-end gap-0 pr-4">
          <BtnOfficialLink></BtnOfficialLink>
          <Setting class="operators"></Setting>
        </div>
      </div>
  </header>
</template>

<script lang="ts" setup>
import Home from "../operators/Home.vue";
import BtnOfficialLink from "../components/BtnOfficialLink.vue";
import { useRoute } from "vue-router";
import { computed } from "vue";
import Preload from "../api/Preload";
import RouteBox from "../entities/RouteBox";
import Edit from "../operators/Edit.vue";
import Add from "../operators/Add.vue";
import Toast from "./Toast.vue";
import { useNodeStore } from "../stores/NodeStore";
import useEditorStore from "../stores/EditorStore";
import Toolbar from "./Toolbar.vue";
import More from "../operators/More.vue";
import Setting from "../operators/Setting.vue";

const editorStore = useEditorStore()
const route = useRoute();
const isWindows = Preload.isWindows();
const isSetting = computed(() => route.name?.toString().startsWith('setting'));
const current = computed(() => useNodeStore().current);
const editable = computed(() => route.name == 'nodes.edit')
const editor = computed(() => editorStore.editor);
const isShop = computed(() => route.params.tree =='shop')
</script>

<style scoped lang="postcss">
.operators {
  @apply btn-ghost btn-sm flex items-center rounded px-2
}
</style>