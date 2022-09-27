<script setup lang="ts">
import creatorData from '@/assets/creator_data.json'
import tankiData from '@/assets/tanki_data.json'
import { KrmItem } from '@/types'

const route = useRoute()
const radicalNumber = route.params.radical_num as string
const jsonFilePath = "../krm/Radical_" + ('000' + radicalNumber).slice(-3) + ".json";
const { data, pending } = await useFetch<KrmItem[]>(jsonFilePath, { initialCache: true, server: false })

function getHdicGwPage(krid: string) {
  // https://glyphwiki.org/wiki/hdic_hkrm-01001310
  return "https://glyphwiki.org/wiki/hdic_hkrm-" + krid.substring(1)
}
function getHdicGwImage(krid: string) {
  // https://glyphwiki.org/glyph/hdic_hkrm-01001310.png
  return "https://glyphwiki.org/glyph/hdic_hkrm-" + krid.substring(1) + ".png"
}

function getCreatorGwPage(krid: string, radicalNumber: string, postion: number) {
  // https://glyphwiki.org/wiki/otakusei_hkrm-05047410
  const creator = creatorData.filter(item => item.radical_num === radicalNumber).filter(item => parseInt(item.start) <= postion && parseInt(item.end) >= postion)
  const tanki = tankiData.filter(item => item.radical_num === radicalNumber).filter(item => parseInt(item.start) <= postion && parseInt(item.end) >= postion)
  let username: string
  if (creator.length > 0) {
    username = creator[0].username
  }
  if (tanki.length > 0) {
    username = tanki[0].username
  }
  return `https://glyphwiki.org/wiki/${username}_hkrm-` + krid.substring(1)
}

function getCreatorGwImage(krid: string, radicalNumber: string, postion: number) {
  // https://glyphwiki.org/wiki/otakusei_hkrm-05047410
  const creator = creatorData.filter(item => item.radical_num === radicalNumber).filter(item => parseInt(item.start) <= postion && parseInt(item.end) >= postion)
  const tanki = tankiData.filter(item => item.radical_num === radicalNumber).filter(item => parseInt(item.start) <= postion && parseInt(item.end) >= postion)

  let username: string
  if (creator.length > 0) {
    username = creator[0].username
  } 
  if (tanki.length > 0) {
    username = tanki[0].username
  }
  return `https://glyphwiki.org/glyph/${username}_hkrm-` + krid.substring(1) + ".png"
}
function getOriginImage(sid: string) {
  // https://viewer.hdic.jp/img/krm/sid/S00001
  return "https://viewer.hdic.jp/img/krm/sid/" + sid
}

</script>

<template>
  <div class="container flex  mx-auto justify-center items-center">
    <div class="flex flex-col w-full items-center">
      <div v-if="!pending" v-for="(item,index) of data" class="flex gap-2">
        <div>{{index+1}}</div>
        <div>
          <p class=" text-3xl">{{item.Entry}}</p>
        </div>
        <div>
          <img :src="getOriginImage(item.KRID_sn)" alt="" class="h-24">
        </div>
        <div>
          <a :href="getCreatorGwPage(item.KRID,radicalNumber,index+1)">
            <img :src="getCreatorGwImage(item.KRID,radicalNumber,index+1)" alt="" class="h-24">
          </a>

        </div>

        <div>
          <a href="#"><span> >> </span></a>
        </div>

        <div>
          <a :href="getHdicGwPage(item.KRID)">
            <img :src="getHdicGwImage(item.KRID)" alt="" class="h-24">
          </a>
        </div>
      </div>
    </div>

  </div>
</template>