<script setup lang="ts">
import creatorData from '@/assets/creator_data.json'
import tankiData from '@/assets/tanki_data.json'
import { KrmItem, GwApiBody } from '@/types'

const route = useRoute()
const radicalNumber = route.params.radical_num as string
const jsonFilePath = "../krm/Radical_" + ('000' + radicalNumber).slice(-3) + ".json";
const { data, pending } = await useFetch<KrmItem[]>(jsonFilePath, { initialCache: true, server: false })

function getHdicGwPage(krid: string) {
  return "https://glyphwiki.org/wiki/hdic_hkrm-" + krid.substring(1)
}
function getHdicGwImage(krid: string) {
  return "https://glyphwiki.org/glyph/hdic_hkrm-" + krid.substring(1) + ".png"
}

function getGwName(krid: string, radicalNumber: string, postion: number) {
  // this.tantou+'_hkrm-'+krid
  const creator = creatorData.filter(item => item.radical_num === radicalNumber).filter(item => parseInt(item.start) <= postion && parseInt(item.end) >= postion)
  const tanki = tankiData.filter(item => item.radical_num === radicalNumber).filter(item => parseInt(item.start) <= postion && parseInt(item.end) >= postion)
  let username: string

  if (tanki.length > 0) {
    username = tanki[0].username
  }
  if (creator.length > 0) {
    username = creator[0].username
  }
  return `${username}_hkrm-` + krid.substring(1)
}

function getCreatorGwPage(krid: string, radicalNumber: string, postion: number) {
  const gwName = getGwName(krid, radicalNumber, postion)
  return `https://glyphwiki.org/wiki/${gwName}`
}

function getCreatorGwImage(krid: string, radicalNumber: string, postion: number) {
  const gwName = getGwName(krid, radicalNumber, postion)
  return `https://glyphwiki.org/glyph/${gwName}.png`
}
function getOriginImage(sid: string) {
  return "https://viewer.hdic.jp/img/krm/sid/" + sid
}

async function gotoGwEdit(krid: string, radicalNumber: string, postion: number, entry: string) {
  const gwName = getGwName(krid, radicalNumber, postion)
  const url = `https://glyphwiki.org/api/glyph?name=${gwName}`
  const { data } = await useFetch<GwApiBody>(url, { server: false, initialCache: false })
  const editUrl = `https://glyphwiki.org/kage-editor/#name=hdic_${gwName.split("_")[1]}&data=${data.value.data}&related=${entry}&edittime=`
  window.open(editUrl, '_blank');
}
</script>

<template>
  <div class="container flex  mx-auto justify-center items-center pt-4">
    <div class="w-full overflow-x-auto ">
      <table class="table w-full">
        <thead>
          <tr>
            <th>順</th>
            <th>原本画像</th>
            <th>担当者作成字形</th>
            <th></th>
            <th>登録字形</th>
            <th>掲出字・注文</th>

          </tr>
        </thead>
        <tbody>
          <tr v-for="(item,index) of data" class="hover">
            <th>{{index+1}}</th>
            <td>
              <img :src="getOriginImage(item.KRID_sn)" class="h-24">
            </td>
            <td>
              <a :href="getCreatorGwPage(item.KRID,radicalNumber,index+1)" target="_blank">
                <img :src="getCreatorGwImage(item.KRID,radicalNumber,index+1)" class="h-24">
              </a>
            </td>
            <td>
              <button class="btn btn-success"
                @click="gotoGwEdit(item.KRID,radicalNumber,index+1,item.Entry)">>></button>
            </td>
            <td>
              <a :href="getHdicGwPage(item.KRID)" target="_blank">
                <img :src="getHdicGwImage(item.KRID)" class="h-24">
              </a>
            </td>
            <td>
              <div class="w-20">
                <div class="text-3xl">{{item.Entry}}</div>
                <div class="text-xs">{{item.Def}}</div>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>