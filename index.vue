<template>
  <div>
    <h1>kim sang ki223</h1>
  </div>
  <div>
    <!-- 메인 메뉴 항목, 클릭 시 서브메뉴 표시 상태 토글 -->
    <q-item clickable
      @click="toggleChildren">
      <q-item-section v-if="icon"
        avatar>
        <q-icon :name="icon" />
      </q-item-section>

      <q-item-section>
        <q-item-label>{{ title }}</q-item-label>
        <q-item-label caption>{{ caption }}</q-item-label>
      </q-item-section>

      <!-- 서브메뉴 토글 아이콘 (예: 화살표) -->
      <q-item-section side
        v-if="children.length">
        <q-icon name="expand_more" />
      </q-item-section>
    </q-item>

    <!-- 서브메뉴 애니메이션 적용 -->
    <transition name="sub-menu">
      <q-list v-if="showChildren"
        class="sub-menu">
        <q-item v-for="(child, index) in children"
          :key="index"
          clickable
          tag="a"
          target="_blank"
          :href="child.link">
          <q-item-section v-if="child.icon"
            avatar>
            <q-icon :name="child.icon" />
          </q-item-section>

          <q-item-section>
            <q-item-label>{{ child.title }}</q-item-label>
            <q-item-label caption>{{ child.caption }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </transition>
  </div>
</template>


<script setup>
import { ref, defineProps } from 'vue';

// props 정의
const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  caption: {
    type: String,
    default: '',
  },
  link: {
    type: String,
    default: '#',
  },
  icon: {
    type: String,
    default: '',
  },
  children: {
    type: Array,
    default: () => [],
  },
});

// 서브메뉴 표시 상태를 관리하는 반응형 속성
const showChildren = ref(false);

// 항목 클릭 시 서브메뉴 표시 상태 토글
const toggleChildren = () => {
  showChildren.value = !showChildren.value;
};
</script>

<style scoped>
.sub-menu-enter-active,
.sub-menu-leave-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
  opacity: 0;
  transform: translateX(-20px);
  /* 변경된 부분 */
}

.sub-menu {
  margin-left: 20px;
  /* 서브 메뉴를 오른쪽으로 20px 이동 */
}

.sub-menu-enter-to,
.sub-menu-leave-to {
  opacity: 1;
  transform: translateX(0);
}
</style>
