<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md row q-gutter-md">
      <q-card dark class="bg-primary">
        <q-card-section>
          <div class="text-h6 text-center">Лабараторные работы по языку JavaScript</div>
          <div class="text-subtitle2 text-center">ст. Шупляк Богдан</div>
          <div class="text-subtitle2 text-center"> гр. ИПЗ-119м</div>
        </q-card-section>
      </q-card>
    </div>
    <div class="flex q-px-lg q-pb-md">
      <q-timeline color="secondary">
        <q-timeline-entry heading>
          Список лабораторных работ
        </q-timeline-entry>

        <q-timeline-entry title=" Морской бой "></q-timeline-entry>
        <q-timeline-entry title=" Условия и работа с формами "></q-timeline-entry>
      </q-timeline>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
}
</script>
