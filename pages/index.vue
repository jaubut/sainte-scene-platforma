<template>
  <div>
    <menu1></menu1>
    <cover1
    :headline="cover.fields.headline"
    :image="cover.fields.image.fields.file.url"
    :text="cover.fields.text"
    :link1="cover.fields.link1"
    :textlink1="cover.fields.linkTitle1"
    ></cover1>
    <center1
    :tagline="center.fields.tagline"
    :headline="center.fields.headline"
    :link1="center.fields.link"
    linktitle="action"
    ></center1>
    <right7></right7>
    <cover1
    :headline="cover.fields.headline"
    :image="cover.fields.image.fields.file.url"
    :text="cover.fields.text"
    :link1="cover.fields.link1"
    :textlink1="cover.fields.linkTitle1"
    ></cover1>
    <texts2></texts2>
    <grids8></grids8>
    <texts2></texts2>
    <grids18></grids18>
    <cover3></cover3>
    <div class="container">
      <vue-instagram class="row py-4" token="5476375392.f9b60dd.4226cf27c1134e348ca8ef4dc51a96bf" :count="8" mediaType="image">
        <template v-slot:feeds="props">
          <div class="col-12 col-md-3 gallery-item">
            <img class="w-100" :src="props.feed.images.standard_resolution.url" />
          </div>
        </template>
      </vue-instagram>
    </div>
    <footers1></footers1>
  </div>
</template>

<script>

import {createClient} from '@/plugins/contentful.js'
import VueInstagram from 'vue-instagram'

const client = createClient()

export default {
  components: {
    VueInstagram
  },
  // `env` is available in the context object
  asyncData ({env}) {
    return Promise.all([
      // fetch all blog posts sorted by creation date
      client.getEntries({
        'content_type': env.CTF_BLOG_POST_TYPE_ID,
        order: '-sys.createdAt'
      }),
      // fetch covers sorted by creation date
      client.getEntries({
        'content_tyle': env.CTF_COVER_TYPE_ID,
        order: '-sys.createdAt'
      })
    ]).then(([center, covers]) => {
      // return data that should be available
      // in the template
      return {
        center: center.items[0],
        cover: covers.items[0]
      }
    }).catch(console.error)
  }
}
</script>

<style>

</style>
