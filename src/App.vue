<template>
  <main class="main">
    <div class="container">
      <div class="main__box">
        <n-data-table
          ref="table"
          :columns="columns"
          :data="data"
          class="table"
        />
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { h, ref } from "vue";
import { NSwitch, NDatePicker, NInputNumber } from "naive-ui";
import type { DataTableColumns } from "naive-ui";

type RowData = {
  key: number;
  title: string;
  sorter: string;
  id: number;
  steName: string;
  isActual: boolean;
  priceEndDate: string;
  priceNotNds: number;
  nds: number;
  price: string;
  fillEndDate: string;
};

const columns: DataTableColumns<RowData> = [
  {
    key: "steName",
    title: "Наименование СТЕ",
    sorter: "default",
  },
  {
    key: "isActual",
    title: "В наличии",
    align: "center",
    width: 120,
    render(row, index) {
      return h(NSwitch, {
        value: row.isActual,
        onUpdateValue(v) {
          data.value[index].isActual = v;
        },
      });
    },
  },
  {
    key: "priceEndDate",
    title: "Срок действия предоставленных сведений",
    width: 200,
    render(row, index) {
      return h(NDatePicker, {
        value: row.priceEndDate,
        placeholder: "Выберите дату",
        bordered: false,
        onUpdateValue(v) {
          data.value[index].priceEndDate = v;
        },
      });
    },
  },
  {
    key: "priceNotNds",
    title: "Цена, руб, без НДС",
    width: 180,
    render(row, index) {
      return h(NInputNumber, {
        value: row.priceNotNds,
        placeholder: "Введите значение",
        bordered: false,
        showButton: false,
        onUpdateValue(v) {
          data.value[index].priceNotNds = v;
        },
      });
    },
  },
  {
    key: "nds",
    title: "НДС, %",
    width: 180,
    render(row, index) {
      return h(NInputNumber, {
        value: row.nds,
        placeholder: "Введите значение",
        bordered: false,
        showButton: false,
        onUpdateValue(v) {
          data.value[index].nds = v;
        },
      });
    },
  },
  {
    key: "price",
    title: "Цена, руб, с НДС",
    width: 150,
    render(row) {
      const price = row.priceNotNds + (row.priceNotNds * row.nds) / 100;
      return price ? price : "";
    },
  },
  {
    key: "fillEndDate",
    title: "Срок заполнения",
    width: 150,
  },
];

const data: RowData[] = ref([
  {
    key: 0,
    id: 1,
    steName: "АЗОТ ГАЗООБРАЗНЫЙ СОРТ - ПЕРВЫЙ ТЕХНИЧЕСКИЙ БАЛОН 50л",
    isActual: false,
    priceEndDate: null,
    priceNotNds: null,
    nds: null,
    price: null,
    fillEndDate: "05.05.2005",
  },
  {
    key: 1,
    id: 2,
    steName:
      "OZONE MICRONE H-67 НАБОР ФИЛЬТРОВ ДЛЯ ПЫЛЕСОСОВ ELEXTROLUX CYCLONE",
    isActual: false,
    priceEndDate: null,
    priceNotNds: null,
    nds: null,
    price: null,
    fillEndDate: "12.12.2012",
  },
  {
    key: 2,
    id: 3,
    steName:
      "OZONE MICRONE H-67 НАБОР ФИЛЬТРОВ ДЛЯ ПЫЛЕСОСОВ ELEXTROLUX CYCLONE",
    isActual: false,
    priceEndDate: null,
    priceNotNds: null,
    nds: null,
    price: null,
    fillEndDate: "07.07.2007",
  },
]);
</script>

<style lang="scss" scoped>
.main {
  width: 100%;

  &__box {
    display: flex;
  }
}

.table {
  ::v-deep(.n-data-table-table) {
    .n-data-table-th {
      text-align: center;
      text-transform: uppercase;
      font-weight: 600;
      color: white;
      background: #4e82e8;
      border-right: 1px solid rgba(243, 243, 247, 0.3);

      .n-data-table-sorter {
        color: white;
      }
    }

    .n-data-table-td {
      font-size: 12px;
      line-height: 18px;
      font-weight: 600;
      border-right: 1px solid var(--n-merged-border-color);
    }
  }
}
</style>
