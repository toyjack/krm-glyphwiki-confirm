<template>
  <div class="hero min-h-fit md:min-h-screen bg-base-200">
    <div class="hero-content flex-col lg:flex-row-reverse">
      <div class="tooltip" data-tip="類聚名義抄 - 国立国会図書館デジタルコレクション">
        <a href="https://dl.ndl.go.jp/info:ndljp/pid/2609857">
          <img src="https://www.dl.ndl.go.jp/api/iiif/2586890/F0000004/full/full/0/default.jpg"
            class="max-w-sm rounded-lg shadow-2xl" alt="類聚名義抄 - 国立国会図書館デジタルコレクション" />
        </a>
      </div>
      <div>
        <h1 class="text-5xl font-bold">GlyphWikiによる観智院本『類聚名義抄』字形の再現</h1>
        <p class="py-6">
          平安時代漢字字書総合データベース（HDIC）プロジェクトでは、観智院本『類聚名義抄』（以下、名義抄）の全文テキストデータベースを2022年3月に公開した。
          名義抄は、平安時代の日本語の重要資料であり、その価値は、多数の和訓を収録し日本語の語彙史の資料となること、和訓と漢字の多くに声点が施され音韻史の資料となること、
          漢字には「正」「俗」等の字体注記が豊富で文字史の資料となることにある。名義抄は古写本として伝存するが、その活字翻刻本はいまだ存在しない。
          これは、名義抄に難字が極めて多いことによるが、UnicodeとGlyphWikiとを併用すれば、必要な字形を作字することが可能である。
          ただ、手書きの漢字を明朝体化するに際して、包摂の範囲を明示的に示す必要がある。
          このサイトは、作成した字形の登録と確認のためのものである。
        </p>
        <NuxtLink to="/radicals" class="btn btn-primary">部首リスト</NuxtLink>
      </div>
    </div>
  </div>
</template>