<script setup lang="ts">
import radicalList1 from "~~/assets/radical_data1.json"
import radicalList2 from "~~/assets/radical_data2.json"
import radicalList3 from "~~/assets/radical_data3.json"
</script>

<template>
<div class="container flex flex-col mx-auto">
  <div class="flex gap-5 justify-center pt-4">
    <div class="flex-1">
      <table class="table w-full">
        <thead>
          <tr>
            <td>巻</td>
            <td>部首番号</td>
            <td>部首</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="record of radicalList1">
            <td>{{record.vol}}</td>
            <td>{{record.radical_num}}</td>
            <td>
              <NuxtLink :to="'/radicals/'+record.radical_num" class="text-teal-500 underline">{{record.radical}}</NuxtLink>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="flex-1">
      <table class="table w-full">
        <thead>
          <tr>
            <td>巻</td>
            <td>部首番号</td>
            <td>部首</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="record of radicalList2">
            <td>{{record.vol}}</td>
            <td>{{record.radical_num}}</td>
            <td>
              <NuxtLink :to="'/radicals/'+record.radical_num" class="text-teal-500 underline">{{record.radical}}</NuxtLink>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="flex-1">
      <table class="table w-full">
        <thead>
          <tr>
            <td>巻</td>
            <td>部首番号</td>
            <td>部首</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="record of radicalList3">
            <td>{{record.vol}}</td>
            <td>{{record.radical_num}}</td>
            <td>
              <NuxtLink :to="'/radicals/'+record.radical_num" class="text-teal-500 underline">{{record.radical}}</NuxtLink>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>  
</template>