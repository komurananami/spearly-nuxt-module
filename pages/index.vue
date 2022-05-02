<template>
  <div class="dark:bg-gray-900 mt-6">
    <div class="max-w-screen-lg md:flex mx-auto dark:bg-gray-900">
      <div class="md:w-1/3 p-2 md:flex md:justify-center">
        <AuthorCard />
      </div>
      <div class="md:w-2/3 px-8">
        <AuthorIntro></AuthorIntro>
        <Expertise></Expertise>
        <TimeLine></TimeLine>

        <spearly-form id="f-5CXBGn30HWINKdc9twRT">
          <template v-slot="form">
            <fieldset
              v-for="field in form.fields"
              :key="field.identifier"
              class="f-fieldset"
            >
              <label :for="field.identifier">
                {{ field.name }}
                <i v-if="field.required">*</i>
              </label>

              <input
                v-if="field.inputType === 'text'"
                :id="field.identifier"
                v-model="answers[field.identifier]"
                :required="field.required"
                type="text"
                :placeholder="field.description"
                class="f-input"
              />
              <textarea
                v-else-if="field.inputType === 'text_area'"
                :id="field.identifier"
                v-model="answers[field.identifier]"
                :required="field.required"
                :placeholder="field.description"
                class="f-input"
              />
            </fieldset>

            <input
              v-model="answers._spearly_gotcha"
              type="text"
              style="
                position: absolute;
                width: 1px;
                height: 1px;
                overflow: hidden;
              "
            />
            <button @click="form.submit(answers)" class="f-btn">送信</button>
          </template>
        </spearly-form>
      </div>
    </div>
  </div>
</template>

<script>
import siteMetaInfo from "@/data/sitemetainfo";
export default {
  data() {
    return {
      siteMetaInfo: siteMetaInfo,
      answers: {
        name: "",
        email: "",
        form: "",
        _spearly_gotcha: "",
      },
    };
  },
  head: {
    title: siteMetaInfo.title,
    meta: [
      { charset: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        hid: "description",
        name: "description",
        content: siteMetaInfo.description,
      },
    ],
    link: [{ rel: "icon", type: "image/x-icon", href: "/favicon.ico" }],
  },
};
</script>

<style>
.f-input {
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 4px;
  padding: 4px 8px;
}

.f-btn {
  background: #000;
  color: #fff;
  padding: 4px 8px;
  border-radius: 6px;
}

.f-fieldset {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
</style>
