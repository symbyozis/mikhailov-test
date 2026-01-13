<script setup lang="ts">
import { computed, ref } from 'vue';
import Layout from './components/widgets/Layout.vue';
import { leftCollection, rightCollection } from './shared/collections';
import { IItem } from './shared/types';
import Box from './components/features/Box.vue';
import Item from './components/features/Item.vue';
import GridBox from './components/features/GridBox.vue';

const leftBoxItems = ref<IItem[]>(leftCollection)
const rightBoxItems = ref<IItem[]>(rightCollection)

const selectedLeftBoxIds = ref<Set<number>>(new Set())
const selectedRightBoxItem = ref<null | IItem>(null)

const selectedLeftBoxItems = computed(() => leftBoxItems.value.filter(item => selectedLeftBoxIds.value.has(item.id)))

const selectItem = (id: number) => {
  if (selectedLeftBoxIds.value.has(id)) {
    selectedLeftBoxIds.value.delete(id)
  } else if (selectedLeftBoxIds.value.size < 6) {
    selectedLeftBoxIds.value.add(id)
  }
}
</script>

<template>
  <Layout>
    <div class="flex flex-col gap-4">
      <section class="flex gap-4 md:min-h-[20vh]">
        <Box>
          <GridBox>
            <Item v-for="item in selectedLeftBoxItems" :key="item.id" :id="item.id" :name="item.name" />
          </GridBox>
        </Box>
        <Box>
          <Item v-if="selectedRightBoxItem" :id="selectedRightBoxItem.id" :name="selectedRightBoxItem.name" fill />
        </Box>
      </section>
      <section class="flex gap-4 md:min-h-[55vh]">
        <Box>
          <GridBox>
            <Item v-for="item in leftBoxItems" :key="item.id" :id="item.id" :name="item.name"
              :selected="selectedLeftBoxIds.has(item.id)" @click="selectItem(item.id)" />
          </GridBox>
        </Box>
        <Box>
          <GridBox>
            <Item v-for="item in rightBoxItems" :key="item.id" :id="item.id" :name="item.name"
              :selected="item.id === selectedRightBoxItem?.id"
              @click="selectedRightBoxItem = selectedRightBoxItem?.id === item.id ? null : item" />
          </GridBox>
        </Box>
      </section>
    </div>
  </Layout>
</template>
