<template>
  <div class="tableFlex">
    <div class="tableFlex__item">
      <h3>부호화</h3>
      <table class="tableData">
        <thead>
          <tr>
            <th scope="col">순서</th>
            <th scope="col">자극물</th>
            <th scope="col">선택정답</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(r, index) in result1" :key="r.num">
            <td>{{ index + 1 }}</td>
            <td>{{ r.num }}</td>
            <td>{{ r.answer }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="tableFlex__item">
      <h3>인출 | 정답수 : {{ answerCnt }}</h3>
      <table class="tableData">
        <thead>
          <tr>
            <th scope="col">순서</th>
            <th scope="col">자극물</th>
            <th scope="col">방해자극</th>
            <th scope="col">배치순서</th>
            <th scope="col">선택정답</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(r, index) in result2" :key="r.num">
            <td>{{ index + 1 }}</td>
            <td>{{ r.answer }}</td>
            <td>{{ r.extra.join(",") }}</td>
            <td>{{ r.totalArr.join(",") }}</td>
            <td>{{ r.selected }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  props: {
    result1: { type: Array as any, default: [] },
    result2: { type: Array as any, default: [] },
  },
  computed: {
    answerCnt() {
      let correctAnswer = 0;
      this.result2.forEach((el: any) => {
        if (el.answer === el.selected) correctAnswer++;
      });
      return correctAnswer || "";
    },
  },
});
</script>

<style>
.tableData {
  margin: auto;
  border: 1px solid black;
  border-collapse: collapse;
}
.tableFlex {
  display: flex;
  width: 100%;
  font-size: 10px;
  gap: 5px;
}
th,
td {
  border: 1px solid #444444;
}
</style>
