  <template>
  <div class="view-General view-Post">
    <ul class="post-List">
      <li class="post-Item">
        <div v-if="thumbnail" class="post-Thumbnail" @click="showModal = true">
          <img :src="thumbnail">
        </div>
        <div class="post-Info">
          <div v-if="title">
            <h1>{{ title }}</h1>
          </div>
          <div v-if="location">
            <p>&nbsp;— {{ location }}</p>
          </div>
        </div>
        <MarkdownItem v-if="content" :input="content" class="post-Content"/>
        <div v-if="image_0" class="post-Images" @click="showModal = true">
          <img v-if="image_0" :src="image_0">
          <img v-if="image_1" :src="image_1">
          <img v-if="image_2" :src="image_2">
          <img v-if="image_3" :src="image_3">
          <img v-if="image_4" :src="image_4">
          <img v-if="image_5" :src="image_5">
          <img v-if="image_6" :src="image_6">
          <img v-if="image_7" :src="image_7">
          <img v-if="image_8" :src="image_8">
          <img v-if="image_9" :src="image_9">
        </div>
      </li>
    </ul>
    <!-- <div class="post-Footer">
      <div
        v-if="previousProjectId()"
        @click="navigateToProject(previousProjectId())"
        class="post-Footer_Prev"
      >
        <img class="arrow" src="@/assets/images/arrow.png">
        <p>Previous Post</p>
      </div>
      <div
        v-if="nextProjectId()"
        @click="navigateToProject(nextProjectId())"
        class="post-Footer_Next"
      >
        <p>Next</p>
        <img class="arrow" src="@/assets/images/arrow.png">
      </div>
    </div>-->
    <modalItem v-if="showModal" @close="showModal = false">
      <sliderItem
        @close="showModal = false"
        :images="[thumbnail, image_0, image_1, image_2, image_3, image_4, image_5, image_6, image_7, image_8, image_9]"
      ></sliderItem>
    </modalItem>
  </div>
</template>

<script>
import MarkdownItem from '~/components/MarkdownItem.vue'
import SliderItem from '~/components/SliderItem.vue'
import ModalItem from '~/components/ModalItem.vue'

export default {
  components: {
    MarkdownItem,
    SliderItem,
    ModalItem
  },
  data() {
    return {
      showModal: false
    }
  },
  asyncData(context) {
    return context.app.$storyapi
      .get('cdn/stories/blog/' + context.params.postId, {
        version: process.env.NODE_ENV === 'production' ? 'published' : 'draft'
      })
      .then(res => {
        return {
          title: res.data.story.content.title,
          location: res.data.story.content.location,
          content: res.data.story.content.content,
          thumbnail: res.data.story.content.thumbnail,
          image_0: res.data.story.content.image_0,
          image_1: res.data.story.content.image_1,
          image_2: res.data.story.content.image_2,
          image_3: res.data.story.content.image_3,
          image_4: res.data.story.content.image_4,
          image_5: res.data.story.content.image_5,
          image_6: res.data.story.content.image_6,
          image_7: res.data.story.content.image_7,
          image_8: res.data.story.content.image_8,
          image_9: res.data.story.content.image_9
        }
      })
  }
  // methods: {
  //   previousProjectId() {
  //     const project = this.projects[this.getProjectIndex() - 1]
  //     if (project) {
  //       return project.id
  //     } else {
  //       return null
  //     }
  //   },
  //   nextProjectId() {
  //     const project = this.projects[this.getProjectIndex() + 1]
  //     if (project) {
  //       return project.id
  //     } else {
  //       return null
  //     }
  //   },
  //   navigateToProject(id) {
  //     this.$router.push({ path: `/projects/${id}` })
  //   },
  //   getProjectIndex() {
  //     let index = this.projects.findIndex(
  //       element => element.id === this.$route.params.id
  //     )
  //     return index === -1 ? 0 : index
  //   }
  // },
}
</script>

<style lang="sass" scoped>
.view-Project
  margin-top: 100px
  display: flex
  flex-direction: column
  justify-content: center
  align-items: center
.project-List
  display: flex
  flex-direction: column
  width: 500px
  li
    background: lightblue
    margin-bottom: 100px
  img
    width: 100%
    height: auto
</style>
