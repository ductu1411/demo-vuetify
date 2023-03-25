<script setup lang="ts">
import AuthProvider from '@/views/pages/authentication/AuthProvider.vue'
import { useGenerateImageVariant } from '@core/composable/useGenerateImageVariant'
import { VNodeRenderer } from '@layouts/components/VNodeRenderer'
import { themeConfig } from '@themeConfig'
import { emailValidator, regexValidator, requiredValidator } from '@validators'

import authV2LoginIllustrationBorderedDark from '@images/pages/auth-v2-login-illustration-bordered-dark.png'
import authV2LoginIllustrationBorderedLight from '@images/pages/auth-v2-login-illustration-bordered-light.png'
import authV2LoginIllustrationDark from '@images/pages/auth-v2-login-illustration-dark.png'
import authV2LoginIllustrationLight from '@images/pages/auth-v2-login-illustration-light.png'
import authV2MaskDark from '@images/pages/misc-mask-dark.png'
import authV2MaskLight from '@images/pages/misc-mask-light.png'

const authThemeImg = useGenerateImageVariant(authV2LoginIllustrationLight, authV2LoginIllustrationDark, authV2LoginIllustrationBorderedLight, authV2LoginIllustrationBorderedDark, true)

const authThemeMask = useGenerateImageVariant(authV2MaskLight, authV2MaskDark)

const isPasswordVisible = ref(false)
const listPrefixPhoneNumber = ref([{ title: '+972', value: 1 }, { title: '+84', value: 2 }])
const prefixPhoneNumber = ref({ title: '+972', value: 1 })
const regexPhoneNumber = ref('^([0-9]{10})$')
const phoneNumber = ref('0000000000')
const rememberMe = ref(false)
</script>

<template>
  <VRow
    no-gutters
    class="auth-wrapper"
  >
    <VCol
      cols="12"
      lg="12"
      class="d-flex align-center flex-column page-column"
    >
      <div class="page-title">
        <p><b>We</b>Send</p>
      </div>
      <VCard
        flat
        :width="466"
        class="card"
      >
        <VCardText class="title-container">
          <h5 class="text-h5 font-weight-bold mb-1 text-center">
            Sign In
          </h5>
          <div class="mb-0 text-center sub-login-title">
            Enter your phone number to Sign in to your account
          </div>
        </VCardText>
        <VCardText>
          <VForm @submit.prevent="() => {}">
            <div class="d-flex">
              <div class="hidden-arrow-select input-form select-item">
                <VSelect
                  v-model="prefixPhoneNumber"
                  :items="listPrefixPhoneNumber"
                  item-title="title"
                  item-value="value"
                  persistent-hint
                  return-object
                  single-line
                />
              </div>
              <div class="input-form number-item">
                <VTextField
                  v-model="phoneNumber"
                  :rules="[requiredValidator, regexValidator(phoneNumber, regexPhoneNumber)]"
                  type="text"
                />
              </div>
              <div class="button-submit">
                <VBtn
                  block
                  type="submit"
                >
                  Sign In
                </VBtn>
              </div>
            </div>
            <!-- password -->
            <div>
              <div class="d-flex align-center flex-wrap justify-space-between mt-2 mb-4 checkbox">
                <VCheckbox
                  v-model="rememberMe"
                  label="Keep me Sign in"
                />
              </div>
            </div>
          </VForm>
        </VCardText>
      </VCard>
      <div class="sign-up">
        <span>New to WeSend.</span>
        <a
          class="text-primary ms-2"
          href="#"
        >
          Sign up
        </a>
      </div>
      <div class="page-end-title d-flex flex-column-reverse">
        <div>© 2022 We Send. All Rights Reserved.</div>
        <div>Contact Us | Privacy Policy | Terms & Conditions</div>
      </div>
    </VCol>
  </VRow>
</template>

<style lang="scss" scoped>
@use "@core/scss/template/pages/page-auth.scss";
.page-column {
  margin-top: 123px;
  margin-bottom: 80px;
  font-size: 16px;
  color: #374151;
  align-items: center;
  .hidden-arrow-select {
    :deep(.v-field__append-inner)  {
      display: none;
    }
  }
  .card {
    border-radius: 15px;
  }
  .select-item {
    width: 60px;
    margin-right: 8px;
  }
  .input-form {
    :deep(.v-input__control) {
      .v-field--appended {
        padding-inline-end: 0;
      }
      .v-field__input {
        padding: 0;
        border-radius: 5px;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        background: #F3F4FB;
      }
      height: 48px;
      color: #374151;
    }
  }
  .number-item {
    flex: 1;
    margin-right: 8px;
    :deep(.v-input__control) {
      .v-field__input {
        padding-left: 12px;
      }
    }
  }
  .button-submit {
    :deep(.v-btn) {
      background: #111827;
      color: white;
      height: 48px;
    }
  }
  .title-container {
    padding: 42px 0 0 0;
    margin-bottom: 20px;
  }
  .checkbox {
    :deep(.v-label) {
      color: #374151;
    }
  }
  .sign-up {
    margin-top: 33px;
    font-size: 18px;
    line-height: 22px;
    color: #374151;
  }
  .page-end-title {
    flex: 1;
    line-height: 19px;
    gap: 12px;
    align-items: center;
  }
  :deep(.v-btn__content) {
    text-transform: none;
  }
}
</style>

<route lang="yaml">
meta:
  layout: blank
  action: read
  subject: Auth
  redirectIfLoggedIn: true
</route>
