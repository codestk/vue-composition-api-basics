<template>

  <div> 
  <div v-show="step == 1">
    <form action="" class="custom-wffm-form" enctype="multipart/form-data" method="post">
      <div class="row row-flex">
        <div class="col-md-12">
          <div class="title">
            <label>
              {{ obj.Title }}
            </label>
          </div>
          <!-- <div class="subtitle">
            <label class="displaytext">
              {{ obj.SubTitle }}
            </label>
          </div> -->
        </div>
        <div class="col-md-12">
          <div class="form-group">
            <div class="section"></div>
            <div class="subtitle">{{ obj.UploadMsg }}</div>
            <input type="text" id="language" :value="obj.Lang" hidden />
            <div class="file-upload-wrapper" data-text="">
              <input name="file-upload-field" type="file" @change="selectFile" id="fileUpload" onfocus="this.value=''"
                accept=".zip" class="file-upload-field" value="">
              <span class="filename filelabel" v-show="!inputFile">{{ obj.SelectFile }}</span>
              <span class="filename" v-show="inputFile">{{ inputFile }}</span>
            </div>
            <div class="has-danger" v-show="!ValidFileType">{{ obj.ErrMsg[3] }}</div>
            <div class="has-danger" v-show="!ValidFileContent">{{ obj.ErrMsg[4] }}</div>
          </div>
        </div>
        <div class="col-md-12">
          <div class="form-group user-input-wrp">

            <input v-show="showpassword" type="text" class="form-control inputText"
              :class="{ 'form-danger': ValidPassword < 0 }" id="password-input" @input="validate($event)"
              v-model="inputPassword" required />
            <div v-show="showpassword" class="eyeButton">
              <span @click="setPassword(false)" @mousedown="show = !show" @mouseup="show = !show"
                @touchstart="show = !show" @touchend="show = !show" style="cursor: pointer;">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd"
                    d="M17.9792 7.02079C16.4559 5.90433 14.4614 5 12 5C8.64124 5 6.15189 6.6839 4.54289 8.29289C3.73568 9.1001 3.13255 9.90464 2.73045 10.5078C2.52884 10.8102 2.37621 11.0643 2.27238 11.246C2.22043 11.337 2.18057 11.41 2.1528 11.462C2.13891 11.4881 2.12804 11.5089 2.12017 11.5241L2.11062 11.5428L2.10753 11.5489L2.10641 11.5511L2.10596 11.552C2.10576 11.5524 2.10557 11.5528 3 12L2.10557 11.5528C1.96481 11.8343 1.96481 12.1657 2.10557 12.4472L3 12C2.10557 12.4472 2.10576 12.4476 2.10596 12.448L2.10641 12.4489L2.10753 12.4511L2.11062 12.4572L2.12017 12.4759C2.12804 12.4911 2.13891 12.5119 2.1528 12.538C2.18057 12.59 2.22043 12.663 2.27238 12.754C2.37621 12.9357 2.52884 13.1898 2.73045 13.4922C3.13255 14.0954 3.73568 14.8999 4.54289 15.7071C5.26502 16.4292 6.16447 17.1664 7.24025 17.7597L8.72718 16.2728C7.62494 15.7615 6.70214 15.0379 5.95711 14.2929C5.26432 13.6001 4.74245 12.9046 4.39455 12.3828C4.29956 12.2403 4.218 12.1115 4.14991 12C4.218 11.8885 4.29956 11.7597 4.39455 11.6172C4.74245 11.0954 5.26432 10.3999 5.95711 9.70711C7.34811 8.3161 9.35876 7 12 7C13.81 7 15.3239 7.61809 16.5452 8.4548L17.9792 7.02079ZM15.2841 9.71586C14.5614 8.6787 13.36 8 12 8C9.79086 8 8 9.79086 8 12C8 13.36 8.6787 14.5614 9.71586 15.2841L11.1768 13.8232C10.4828 13.5094 10 12.8111 10 12C10 10.8954 10.8954 10 12 10C12.8111 10 13.5094 10.4828 13.8232 11.1768L15.2841 9.71586Z"
                    fill="#9E9E9E" />
                  <path d="M20 5L5 20" stroke="#9E9E9E" stroke-width="2" stroke-linecap="round" />
                  <path fill-rule="evenodd" clip-rule="evenodd"
                    d="M12.0001 17.0001L10.1719 18.8283C10.7495 18.9387 11.359 19.0001 12.0001 19.0001C15.3588 19.0001 17.8482 17.3162 19.4572 15.7072C20.2644 14.9 20.8675 14.0954 21.2696 13.4923C21.4712 13.1899 21.6238 12.9357 21.7277 12.754C21.7796 12.6631 21.8195 12.5901 21.8473 12.5381C21.8611 12.512 21.872 12.4912 21.8799 12.4759L21.8894 12.4573L21.8925 12.4512L21.8936 12.449L21.8941 12.4481C21.8943 12.4477 21.8945 12.4473 21.0001 12.0001L21.8945 12.4473C22.0353 12.1658 22.0353 11.8344 21.8945 11.5529L21.0001 12.0001C21.8945 11.5529 21.8943 11.5525 21.8941 11.5521L21.8936 11.5512L21.8925 11.549L21.8894 11.5429L21.8799 11.5242C21.872 11.509 21.8611 11.4882 21.8473 11.4621C21.8195 11.41 21.7796 11.3371 21.7277 11.2461C21.6238 11.0644 21.4712 10.8103 21.2696 10.5079C20.9753 10.0664 20.5733 9.51706 20.0624 8.93774L18.645 10.3552C19.0463 10.8196 19.3669 11.2593 19.6055 11.6173C19.7005 11.7598 19.7821 11.8886 19.8502 12.0001C19.7821 12.1115 19.7005 12.2404 19.6055 12.3829C19.2576 12.9047 18.7357 13.6002 18.043 14.293C16.652 15.684 14.6413 17.0001 12.0001 17.0001Z"
                    fill="#9E9E9E" />
                </svg></span>
            </div>
            <input v-show="!showpassword" type="password" class="form-control inputText"
              :class="{ 'form-danger': ValidPassword < 0 }" id="password-input" @input="validate($event)"
              v-model="inputPassword" required />
            <div v-show="!showpassword" class="eyeButton">
              <span @click="setPassword(true)" @mousedown="show = !show" @mouseup="show = !show"
                @touchstart="show = !show" @touchend="show = !show" style="cursor: pointer;">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <circle cx="12" cy="12" r="3" stroke="#9E9E9E" stroke-width="2"/>
                  <path d="M21 12C21 12 18 18 12 18C6 18 3 12 3 12C3 12 6 6 12 6C18 6 21 12 21 12Z" stroke="#9E9E9E" stroke-width="2" stroke-linejoin="round"/>
                </svg></span>
            </div>
            <label class="floating-label">{{ obj.Password }}</label>
            <div class="has-danger" v-show="ValidPassword === -1">{{ obj.ErrMsg[1] }}</div>
            <div class="has-danger" v-show="ValidPassword === -2">{{ obj.ErrMsg[2] }}</div>
          </div>
        </div>

        <div class="col-md-12">
          <div class="form-group center-block text-highlight">
            <h2 class="subtitle">{{ obj.InfoTitle }}</h2>
          </div>
        </div>
        <div class="col-md-6">
          <div class="form-group user-input-wrp">
            <input type="text" class="form-control inputText" :class="{ 'form-danger': !ValidName }" id="name-input"
              @input="validate($event)" v-model="inputName" required />
            <label class="floating-label">{{ obj.Name }}</label>
            <div class="has-danger" v-show="!ValidName">{{ obj.NameMsg }}</div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="form-group user-input-wrp">
            <input type="text" class="form-control inputText" :class="{ 'form-danger': !ValidSurname }"
              id="surname-input" @input="validate($event)" v-model="inputSurname" required />
            <label class="floating-label">{{ obj.Surname }}</label>
            <div class="has-danger" v-show="!ValidSurname">{{ obj.SurnameMsg }}</div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="form-group user-input-wrp">
            <input type="text" class="form-control inputText" :class="{ 'form-danger': !ValidMobile }" id="mobile-input"
              @input="validate($event)" v-model="inputMobile" required />
            <label class="floating-label">{{ obj.Mobile }}</label>
            <div class="has-danger" v-show="!ValidMobile">{{ obj.MobileMsg }}</div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="form-group user-input-wrp">
            <input type="text" class="form-control inputText" :class="{ 'form-danger': !ValidEmail }" id="email-input"
              @input="validate($event)" v-model="inputEmail" required />
            <label class="floating-label">{{ obj.Email }}</label>
            <div class="has-danger" v-show="!ValidEmail">{{ obj.EmailMsg }}</div>
          </div>
        </div>

        <div class="col-md-12">
          <div class="form-group">
            <div style="float: left; display: table;margin-top:25px">
              <input id="AcceptPrivacy" name="AcceptPrivacy" type="checkbox" @change="onReadChecked($event)"
                class="form-control option-input checkbox" :disabled="isReading == false" />
            </div>
            <div style="display: table;margin-top:25px">
              <label for="AcceptPrivacy" class="accept-policy-label">
                <section @scroll="onScroll" id="pdpa-section"
                  style="width: 100%; margin: 0px 0px 20px; padding: 0px; height: 140px; overflow: hidden scroll; cursor: text; text-align: left"
                  class="term-con-bottom-pc" v-html="obj.Message"></section>
              </label>
            </div>
          </div>

          <div class="form-group">
            <button type="button" class="btn-default" @click="resetFile">{{ obj.Clear }}</button>
            <span class="span-space-button"></span>
            <button type="button" class="btn-primary" @click="nextStep(2)" :disabled="isChecked == false">{{ obj.Next
            }}</button>
          </div>
        </div>
        <div class="col-md-12">
          <div class="form-group notetext" v-html="obj.Remark"></div>
        </div>
      </div>
    </form>
  </div>

  <!-- Step 2 -->
  <div v-show="step == 2" class="row custom-wffm-form">
    <div class="col-md-12">
      <div class="title">
        <label style="font-size: 26px font-weight: 700"> {{ obj.ResultTitle }} </label>
        <div class="section"></div>
      </div>
    </div>
    <div class="col-md-12">
      <div class="subtitle">
        {{ obj.ResultSubTitle }}
      </div>
    </div>
    <div class="col-md-12">
      <div class="filename">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M13.5 3H6V21H18V7.5M13.5 3L18 7.5M13.5 3V7.5H18" stroke="#003399" stroke-width="2"
            stroke-linejoin="round" />
          <path d="M14 17H8" stroke="#003399" stroke-width="2" />
          <path d="M16 12H8" stroke="#003399" stroke-width="2" />
        </svg>
        <span v-show="inputFile" class="resultfile">{{ inputFile }}</span>
      </div>
    </div>
    <div class="col-md-12">
      <div class="form-group center-block align-left">
        <h2 class="subtitle">{{ obj.InfoTitle }}</h2>
      </div>
    </div>
    <div class="col-md-12">
      <div class="form-group user-input-wrp">
        <label class="show-floating-label">{{ obj.Name }}</label>
        <input type="text" class="form-control noinputText" disabled v-model="inputName" required />
      </div>
    </div>
    <div class="col-md-12">
      <div class="form-group user-input-wrp">
        <label class="show-floating-label">{{ obj.Surname }}</label>
        <input type="text" class="form-control noinputText" disabled v-model="inputSurname" required />
      </div>
    </div>
    <div class="col-md-12">
      <div class="form-group user-input-wrp">
        <label class="show-floating-label">{{ obj.Mobile }}</label>
        <input type="text" class="form-control noinputText" disabled v-model="inputMobile" required />
      </div>
    </div>
    <div class="col-md-12">
      <div class="form-group user-input-wrp">
        <label class="show-floating-label">{{ obj.Email }}</label>
        <input type="email" class="form-control noinputText" disabled v-model="inputEmail" required />
      </div>
    </div>
    <div class="col-md-12">
      <div class="form-group">
        <button type="button" class="btn-default" @click="nextStep(1)">{{ obj.Edit }}</button>
        <span class="span-space-button"></span>
        <button type="button" class="btn-primary" @click="submitFile" :disabled="isChecked == false">{{ obj.Submit
        }}</button>
      </div>
    </div>
  </div>

  <!-- Step 3 Success -->
  <div v-show="step == 3" class="row custom-wffm-form">
    <div class="col-md-12">
      <div class="title">
        <label style="font-size: 26px font-weight: 700"> {{ obj.SuccessTitle }} </label>
        <div class="section"></div>
      </div>
    </div>
    <div class="col-md-12">
      <div class="title"><svg width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="24" cy="24" r="24" fill="#003399" />
          <path d="M16.0004 24.0002L22.0001 29.9998L31.9995 18.0005" stroke="white" stroke-width="2"
            stroke-linecap="round" stroke-linejoin="round" />
        </svg>
      </div>
      <div class="resulttext" v-html="obj.SuccessMsg"></div>
      <div class="col-md-12">
        <div class="go-bottom">
          <div class="form-group">
            <button type="button" class="btn-primary" @click="goHome(obj.HomeURL)">{{ obj.Done }}</button>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Step 4 Failed -->
  <div v-show="step == 4" class="row custom-wffm-form">
    <div class="col-md-12">
      <div class="title">
        <label style="font-size: 26px font-weight: 700"> {{ obj.FailedTitle }} </label>
        <div class="section"></div>
      </div>
    </div>
    <div class="col-md-12">
      <div class="title"><svg width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="24" cy="24" r="24" fill="#BB6967" />
          <rect width="24" height="24" transform="translate(12 12)" fill="#BB6967" />
          <path d="M31 17L17 31" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
          <path d="M17 17L31 31" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
        </svg>
      </div>
      <div class="resulttext" v-html="obj.FailedMsg"></div>
    </div>
    <div class="col-md-12">
      <div class="go-bottom">
        <div class="form-group">
          <button type="button" class="btn-danger" @click="resetFile">{{ obj.TryAgain }}</button>
        </div>
      </div>
    </div>
  </div>
</div>


</template>
<script setup>
import { ref } from "vue"


    // Data model
    let dataLists = ref([])
    let fileInputButton = ref(false)
    let zipPassword = ref(false)
    let inputPassword = ref()
    let inputName = ref()
    let inputSurname = ref()
    let inputMobile = ref()
    let inputEmail = ref()
    let isReading = ref(false)
    let isChecked = ref(false)
    let step = ref(1)
    let showpassword = ref(false)
    let inputFile = ref()

    let ValidFileType = ref(true)
    let ValidFileContent = ref(true)
    let ValidPassword = ref()
    let ValidName = ref()
    let ValidSurname = ref()
    let ValidMobile = ref()
    let ValidEmail = ref()
    let obj = ref(formParam)

    // Internal
    let selectedFile = ""
    let filetype = ""
    let refid = ""
    let companyid = ""
    let records = 0
    let submitjson = null

    ValidFileType.value = true
    ValidFileContent.value = true
    ValidPassword.value = 0
    ValidName.value = true
    ValidSurname.value = true
    ValidMobile.value = true
    ValidEmail.value = true
    inputPassword.value = ""
    inputMobile.value = ""
    inputEmail.value = ""

    const model = (() => {
      return {
        getEntries(file, options) {
          return new zip.ZipReader(new zip.BlobReader(file)).getEntries(options)
        },
        async getURL(entry, options) {
          return URL.createObjectURL(await entry.getData(new zip.BlobWriter(), options))
        },
      }
    })()

    /////////////////
    // Main
    /////////////////
    const chooseFiles = () => {
      resetFile()
      document.getElementById("fileUpload").value = ""
      document.getElementById("fileUpload").click()
      document.getElementById("AcceptPrivacy").checked = false
    }

    const selectFile = async (e) => {
      fileInputButton.value = true
      ValidFileContent.value = true

      dataLists.value = []
      try {
        // encodingInput = true
        selectedFile = e.target.files[0]
        inputFile.value = selectedFile.name
        filetype = await getFileType(selectedFile)
        if (filetype === "zip" /* || filetype === 'rar' */) {
          zipPassword.value = true
        } else {
          zipPassword.value = false
          fileInputButton.value = false
          ValidFileType.value = false
        }
        let container = await document.getElementById("pdpa-section")
        container.scrollTop = 0
      } catch (error) {
        alert(errMsg[0])
      }
    }

    const nextStep = async (s) => {
      if (step.value == 1) {
        ValidPassword.value = true
        validate()
        submitjson = await getJSON()
        if (submitjson === null) ValidFileContent.value = false
        if (submitjson < 0) {
          ValidPassword.value = submitjson
        }
      }
      if (ValidPassword.value === true && validate() && submitjson !== null) step.value = s
    }

    const setPassword = (s) => {
      showpassword.value = s
    }

    const submitFile = async (e) => {
      e.preventDefault()

      // ValidPassword.value = 0
      validate()
      if (ValidPassword.value !== -1 && ValidEmail.value && ValidMobile.value) {
        // let json = await getJSON()
        // if (json < 0)
        //   ValidPassword.value = json
        // else {
        submitjson.Lang = obj._value.Lang
        const requestOptions = {
          method: "POST",
          headers: {
            "Content-Type": "application/json charset=utf-8",
            RequestVerificationToken: document.getElementsByName("__RequestVerificationToken")[0].value,
          },
          body: JSON.stringify(submitjson),
        }
        let response = await fetch("/SingleForm/SingleForm/SaveFormData", requestOptions).catch(error => {
          step.value = 4
          return
        })

        if (response.ok) {
          let result = await response.json();
          if (result[0].Result === 1)
            step.value = 3
          else
            step.value = 4
        } else {
          step.value = 4
          return
        }
        // await fetch("/SingleForm/SingleForm/SaveFormData", requestOptions).then((response) => {
        //   console.log(response.json())
        //   if (response[0] === undefined) {
        //     step.value = 4
        //     return
        //   }
        //   if (response[0].Result === 1) {
        //     // refid = response.json()
        //     step.value = 3
        //   }
        // })
      }
    }

    const resetFile = () => {
      fileInputButton.value = false
      isReading.value = false
      isChecked.value = false
      ValidPassword.value = 0
      ValidFileType.value = true
      ValidFileContent.value = true
      ValidName.value = true
      ValidSurname.value = true
      ValidMobile.value = true
      ValidEmail.value = true
      zipPassword.value = false
      inputFile.value = ""
      inputPassword.value = ""
      inputName.value = ""
      inputSurname.value = ""
      inputMobile.value = ""
      inputEmail.value = ""
      selectedFile = ""
      step.value = 1
      showpassword.value = false
      submitjson = null
      document.getElementById("AcceptPrivacy").checked = false
    }

    ////////////////////////
    // Utility , Validate
    ////////////////////////
    const validate = (e) => {
      if (e === undefined) {
        ValidPassword.value = validatePassword(inputPassword.value) ? true : -1
        ValidName.value = inputName.value === "" || inputName.value === undefined ? false : true
        ValidSurname.value = inputSurname.value === "" || inputSurname.value === undefined ? false : true
        ValidEmail.value = validateEmail(inputEmail.value)
        ValidMobile.value = validateMobile(inputMobile.value)
      } else {
        switch (e.currentTarget.id) {
          case "password-input":
            ValidPassword.value = validatePassword(inputPassword.value) ? true : -1
            break
          case "name-input":
            ValidName.value = validateName(inputName.value)
            break
          case "surname-input":
            ValidSurname.value = validateName(inputSurname.value)
            break
          case "email-input":
            ValidEmail.value = validateEmail(inputEmail.value)
            break
          case "mobile-input":
            ValidMobile.value = validateMobile(inputMobile.value)
            break
        }
      }
      return ValidPassword.value !== -1 && ValidName.value && ValidSurname.value && ValidEmail.value && ValidMobile.value
    }

    const validateName = (name) => {
      if (name === '') return false
      let regex = /^[ก-๙a-zA-Z]+$/
      return regex.test(name)
    }
    const validatePassword = (password) => {
      let regex = /^[A-Za-z0-9\s$&+,:=?@#|'<>.^*()%!-]{4}/
      return regex.test(password)
    }

    const validateEmail = (email) => {
      let regex = /^(([^<>()[\]\\.,:\s@\"]+(\.[^<>()[\]\\.,:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      return regex.test(email)
    }

    const validateMobile = (mobile) => {
      if (mobile.trim().replace(/-/g, "").length !== 10) return false
      let regex = /^[+]*[(]{0}[0]{1}[6,8-9][)]{0}[-\s\./0-9]*$/g
      return regex.test(mobile)
    }

    const onScroll = ({ target: { scrollTop, clientHeight, scrollHeight } }) => {
      if (scrollTop + clientHeight + 2 >= scrollHeight) {
        isReading.value = true
      }
    }

    const onReadChecked = (e) => {
      if (e.target.checked) isChecked.value = true
      else isChecked.value = false
    }

    const goHome = (url) => {
      window.location.href = url
    }

    const csvJSON = (csv) => {
      let tocomma = csv.replace(/\|/g, ",")
      let lines = tocomma.replace(/\n/g, "").split("\r")
      let result = {}
      let master = lines[0].split(",")
      let companyid = master[1]
      let records = master[2]
      let data = { Name: inputName.value, Surname: inputSurname.value, Mobile: inputMobile.value, Email: inputEmail.value, Records: records, CompanyID: companyid, Profile: [] }
      result = data
      if (master.length === 3 && lines[1].split(",").length >= 105) {
        for (let i = 0; i < records; i++) {
          result["Profile"].push(lines[0] + "," + lines[i + 1])
        }
      } else result = {}

      // let headers = lines[0].split(",")
      // for (let i = 1 i < lines.length i++) {
      //   let obj = {}
      //   let currentline = lines[i].split(",")
      //   for (let j = 0 j < headers.length j++) {
      //     obj[headers[j]] = currentline[j]
      //   }
      //   result.push(obj)
      // }
      return JSON.stringify(result) //JSON
    }

    const getJSON = async () => {
      if (inputPassword.value != "" && inputPassword.value != undefined) {
        let myjson = null
        if (filetype == "zip") {
          let entries = await loadZipFiles()
          try {
            for (const entry of entries) {
              let blobURL = await extractZIP(entry, inputPassword.value)
              const response = await fetch(blobURL)
              const data = await getTextFromStream(response.body)
              let json = csvJSON(data)
              if (json !== undefined && json !== "{}") {
                myjson = JSON.parse(json)
              }
            }
          } catch (error) {
            if (error.message === "Invalid password") return -2
          }
        } else {
          // let entries = await loadRarFiles()
          // for (const entry of entries) {
          //   // let json = await extractRAR(e)
          //   myjson.push(JSON.parse(await getRARContents(entry)))
          // }
        }
        return myjson
      } else {
        return -1
      }
    }

    /////////////////
    // ZIP module
    /////////////////
    const loadZipFiles = async (filenameEncoding) => {
      let entryLists = []
      let entries = await model.getEntries(selectedFile, {
        filenameEncoding,
      })
      if (entries && entries.length) {
        // const filenamesUTF8 = Boolean(!entries.find(entry => !entry.filenameUTF8))
        const encrypted = Boolean(entries.find((entry) => entry.encrypted))

        dataLists.value = []
        entries.forEach((e) => {
          dataLists.value.push(e.filename)
          entryLists.push(e)
        })
        return entryLists
      }
    }

    const isUTF8 = (str) => {
      let cnt = 0
      for (var i = 0; i < str.length; i++) {
        if (str[i] == 0xe0 && (str[i + 1] == 0xb8 || str[i + 1] == 0xb9)) {
          cnt++
          if (cnt > 6) return true
        }
      }
      return false
    }

    const getTextFromStream = async (readableStream) => {
      let reader = readableStream.getReader()
      let utf8Decoder = new TextDecoder("UTF-8")
      let asciiDecoder = new TextDecoder("windows-874")
      let nextChunk

      let resultStr = ""

      while (!(nextChunk = await reader.read()).done) {
        let partialData = nextChunk.value
        if (isUTF8(partialData)) resultStr += utf8Decoder.decode(partialData)
        else resultStr += asciiDecoder.decode(partialData)
      }

      return resultStr
    }

    const extractZIP = async (entry, passwd) => {
      const controller = new AbortController()
      const signal = controller.signal
      try {
        const blobURL = await model.getURL(entry, {
          password: passwd,
          onprogress: (index, max) => {
            // unzipProgress.value = index
            // unzipProgress.max = max
          },
          signal,
        })
        return blobURL
      } catch (error) {
        if (!signal.reason || signal.reason.code != error.code) {
          throw error
        }
      }
    }

    /////////////////
    // RAR module
    /////////////////
    // const loadRarFiles = async (filenameEncoding) => {
    //   let entryLists = []
    //   return new Promise((resolve) => {
    //     archiveOpenFile(selectedFile, inputPassword.value, (archive, err) => {
    //       dataLists.value = []
    //       archive.entries.forEach((e) => {
    //         dataLists.value.push(e.name)
    //         entryLists.push(e)
    //       })
    //       resolve(entryLists)
    //     })
    //   })
    // }

    // const getRARContents = async (entry) => {
    //   let newjson = ''
    //   let url = ''
    //   return new Promise((resolve) => {
    //     entry.readData(async (data, err) => {
    //       url = URL.createObjectURL(new Blob([data]))
    //       const response = await fetch(url)
    //       const res = await response.text()
    //       let json = await csvJSON(res)
    //       if (json !== undefined && json !== null) {
    //         newjson = '{\"' + entry.name.split('.')[0] + '\" :' + json + '}'
    //         resolve(newjson)
    //       }
    //     })
    //   })
    // }

    // const archiveOpenFile = (file, password, cb) => {
    //   // Get the file's info
    //   let blob = file.slice()
    //   let file_name = file.name
    //   password = password || null

    //   // Convert the blob into an array buffer
    //   let reader = new FileReader()
    //   reader.onload = (evt) => {
    //     let array_buffer = reader.result

    //     // Open the file as an archive
    //     try {
    //       let archive = archiveOpenArrayBuffer(file_name, password, array_buffer)
    //       cb(archive, null)
    //     } catch (e) {
    //       cb(null, e)
    //     }
    //   }
    //   reader.readAsArrayBuffer(blob)
    // }

    // const archiveOpenArrayBuffer = (file_name, password, array_buffer) => {

    //   // Get the entries
    //   let handle = null
    //   let entries = []

    //   handle = _rarOpen(file_name, password, array_buffer)
    //   entries = _rarGetEntries(handle)

    //   // Sort the entries by name
    //   // entries.sort(function (a, b) {
    //   //   if (a.name < b.name) return -1
    //   //   if (a.name > b.name) return 1
    //   //   return 0
    //   // })

    //   // Return the archive object
    //   return {
    //     file_name: file_name,
    //     // archive_type: archive_type,
    //     array_buffer: array_buffer,
    //     entries: entries,
    //     handle: handle
    //   }
    // }

    // const _rarOpen = (file_name, password, array_buffer) => {
    //   // Create an array of rar files
    //   let rar_files = [{
    //     name: file_name,
    //     size: array_buffer.byteLength,
    //     type: '',
    //     content: new Uint8Array(array_buffer)
    //   }]

    //   // Return rar handle
    //   return {
    //     file_name: file_name,
    //     array_buffer: array_buffer,
    //     password: password,
    //     rar_files: rar_files
    //   }
    // }

    // const _rarGetEntries = (rar_handle) => {
    //   // Get the entries
    //   let info = readRARFileNames(rar_handle.rar_files, rar_handle.password)
    //   let entries = []
    //   Object.keys(info).forEach((i) => {
    //     let name = info[i].name
    //     let is_file = info[i].is_file

    //     entries.push({
    //       name: name,
    //       is_file: info[i].is_file,
    //       size_compressed: info[i].size_compressed,
    //       size_uncompressed: info[i].size_uncompressed,
    //       readData: (cb) => {
    //         setTimeout(() => {
    //           if (is_file) {
    //             try {
    //               readRARContent(rar_handle.rar_files, rar_handle.password, name, cb)
    //             } catch (e) {
    //               cb(null, e)
    //             }
    //           } else {
    //             cb(null, null)
    //           }
    //         }, 0)
    //       }
    //     })
    //   })

    //   return entries
    // }

    /////////////////
    // File type
    /////////////////
    const getFileType = async (file) => {
      return new Promise((resolve) => {
        openArchive(file, (archive) => {
          resolve(archive)
        })
      })
    }

    const openArchive = async (file, cb) => {
      // Get the file's info
      let blob = file.slice()

      // Convert the blob into an array buffer
      let reader = new FileReader()
      reader.onload = (evt) => {
        let array_buffer = reader.result

        // Open the file as an archive
        let archive_type = null
        // if (_isRarFile(array_buffer)) {
        //   archive_type = 'rar'
        // } else
        if (_isZipFile(array_buffer)) {
          archive_type = "zip"
        } else {
          archive_type = ""
          // throw new Error("The archive type is unknown")
        }
        cb(archive_type)
      }
      reader.readAsArrayBuffer(blob)
    }

    // const _isRarFile = (array_buffer) => {
    //   // The three styles of RAR headers
    //   let rar_header1 = saneJoin([0x52, 0x45, 0x7E, 0x5E], ', ') // old
    //   let rar_header2 = saneJoin([0x52, 0x61, 0x72, 0x21, 0x1A, 0x07, 0x00], ', ') // 1.5 to 4.0
    //   let rar_header3 = saneJoin([0x52, 0x61, 0x72, 0x21, 0x1A, 0x07, 0x01, 0x00], ', ') // 5.0

    //   // Just return false if the file is smaller than the header
    //   if (array_buffer.byteLength < 8) {
    //     return false
    //   }

    //   // Return true if the header matches one of the RAR headers
    //   let header1 = saneJoin(new Uint8Array(array_buffer).slice(0, 4), ', ')
    //   let header2 = saneJoin(new Uint8Array(array_buffer).slice(0, 7), ', ')
    //   let header3 = saneJoin(new Uint8Array(array_buffer).slice(0, 8), ', ')
    //   return (header1 === rar_header1 || header2 === rar_header2 || header3 === rar_header3)
    // }

    const _isZipFile = (array_buffer) => {
      // The ZIP header
      let zip_header = saneJoin([0x50, 0x4b, 0x03, 0x04], ", ")

      // Just return false if the file is smaller than the header
      if (array_buffer.byteLength < 4) {
        return false
      }

      // Return true if the header matches the ZIP header
      let header = saneJoin(new Uint8Array(array_buffer).slice(0, 4), ", ")
      return header === zip_header
    }

    const saneJoin = (array, separator) => {
      let retval = ""
      for (let i = 0; i < array.length; ++i) {
        if (i === 0) {
          retval += array[i]
        } else {
          retval += separator + array[i]
        }
      }
      return retval
    }

    /////////////////////
    // Model & function
    /////////////////////
    return {
      dataLists,
      zipPassword,
      fileInputButton,
      inputPassword,
      inputName,
      inputSurname,
      inputMobile,
      inputEmail,
      isReading,
      isChecked,
      step,
      showpassword,
      inputFile,

      ValidFileType,
      ValidFileContent,
      ValidPassword,
      ValidName,
      ValidSurname,
      ValidMobile,
      ValidEmail,
      obj,

      onReadChecked,
      onScroll,
      chooseFiles,
      selectFile,
      nextStep,
      setPassword,
      submitFile,
      resetFile,
      validate,
      validatePassword,
      validateEmail,
      validateMobile,
      goHome
    }

</script>

<style scoped>
.row-flex {
  display: flex;
  flex-wrap: wrap;
}

.form-group {
  font-family: "BangkokBank-Regular", Tahoma, Helvetica, Arial, sans-serif !important;
  overflow: hidden;
  position: relative;
  padding: 0;
  text-align: center;
}

#file-input-button {
  width: 100%;
}

#AcceptPrivacy {
  padding: 12px !important;
  border: 1px solid #999 !important;
}

#AcceptPrivacy:hover {
  border: 1px solid #039 !important;
  color: #039 !important;
}

#AcceptPrivacy:checked::before {
  position: absolute;
  content: "✔";
  display: inline-block;
  font-size: 16px;
  line-height: 20px;
  left: 3px !important;
  top: 2px !important;
  color: #039;
}

#AcceptPrivacy:checked {
  border: 1px solid #039 !important;
}

.accept-policy-label {
  line-height: 1.5rem;
}

.title {
  text-align: center;
  font-size: 1.768rem;
  font-weight: bold;
}

.subtitle {
  margin: 10px 0 10px 0;
  line-height: 22px;
  font-size: 1rem;
}

.displaytext {
  font-size: 1rem;
  line-height: 22px;
  text-align: left;
}

.resulttext {
  font-size: 1rem;
  line-height: 22px;
  text-align: center;
  margin-top: 25px;
}

.notetext {
  font-size: 0.768rem;
  line-height: 22px;
  text-align: left;
}

.notetext ::v-deep(ul li) {
  padding-left: 1em;
  padding-bottom: 0.4em;
  position: relative;
}

.notetext ::v-deep(ul li:before) {
  content: '-';
  position: absolute;
  left: 0;
}

.eyeButton {
  position: absolute;
  right: 17px;
  top: 21px;
}

.filename {
  margin: 10px 0 10px 0;
  z-index: 99;
  position: relative;
  top: 14px;
}

.filelabel {
  color: #999;
}


.btn-primary[disabled]:hover,
.btn-default[disabled]:hover {
  background: #4c70b7;
}

[class*="btn-primary"]:hover,
[class*="btn-default"]:hover {
  background: #003fbd;
}

.btn-danger {
  color: #fff;
  background-color: #BB6967;
  border-color: #BB6967;
}

.btn-danger:hover {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}

.go-bottom {
  margin-top: 108px;
}

/* width */
::-webkit-scrollbar {
  width: 8px;
  border-radius: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 2px rgb(223, 223, 223);
  border-radius: 10px;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: rgb(223, 223, 223);
  border-radius: 10px;
}

[class*='btn-primary'] {
  color: #fff;
}

.align-left {
  margin-top: 15px;
  text-align: left;
  font-weight: normal !important;
}

.resultfile {
  margin: 0px 0px 0px 10px;
  position: relative;
  top: -5px;
}

.user-input-wrp {
  position: relative;
  color: #999;
}

.user-input-wrp .inputText {
  width: 100%;
  outline: none;
  border: 1px solid #999;
  /* border-bottom: 1px solid #777 */
  box-shadow: none !important;
  margin: 10px 0 0px 0;
}

.user-input-wrp .inputText:focus {
  border-color: blue;
  /* border-width: medium medium 2px */
}

.user-input-wrp .floating-label {
  position: absolute;
  pointer-events: none;
  top: 24px;
  left: 21px;
  transition: 0.2s ease all;
}

.user-input-wrp .show-floating-label {
  position: absolute;
  font-size: 13px;
  background: #fff;
  padding: 0 5px 0 5px;
  pointer-events: none;
  top: -1px;
  left: 21px;
  transition: 0.2s ease all;
  color: #606060;
}

.user-input-wrp .noinputText {
  width: 100%;
  outline: none;
  border: none;
  /* border-bottom: 1px solid #777 */
  box-shadow: none !important;
  margin: 5px 0 0 5px;
  color: #039;
}

.user-input-wrp input:focus~.floating-label,
.user-input-wrp input:not(:focus):valid~.floating-label {
  background: #fff;
  padding: 0 5px 0 5px;
  top: 4px;
  left: 16px;
  font-size: 13px;
  opacity: 1;
  z-index: 99;
  color: #606060;
}

.text-highlight {
  display: block !important;
  text-align: left;
  font-size: 1rem;
  cursor: text !important;
  color: #585858;
  margin-top: 5px;
  font-weight: bold;
}

.custom-wffm-form [class*="btn"],
.general-form [class*="btn"] {
  margin: 5px 0;
}

button {
  border: 1px solid #ccc;
}

button:hover {
  color: #fff;
  background-color: #039;
}

.term-con-bottom-pc {
  -ms-overflow-style: scrollbar;
  -ms-overflow-x: hidden;
  -ms-overflow-y: scroll;
}

.term-con-bottom-mobile {
  -ms-overflow-style: scrollbar;
  -ms-overflow-x: hidden;
  -ms-overflow-y: scroll;
}

input[type="checkbox"]:disabled {
  background: #ebebeb;
}

input[type="checkbox"]:disabled:hover {
  cursor: not-allowed;
}

.term-con-bottom-pc {
  -ms-overflow-style: scrollbar;
  -ms-overflow-x: hidden;
  -ms-overflow-y: scroll;
}

.term-con-bottom-mobile {
  -ms-overflow-style: scrollbar;
  -ms-overflow-x: hidden;
  -ms-overflow-y: scroll;
}

.select select {
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  display: block;
  padding: 1.2em 3em 1.3em 1.5em;
  margin: 0;
  transition: border-color 0.2s;
  border-radius: 5px;
  background: #fff;
  color: #555 !important;
  line-height: normal;
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
  font-size: 1rem;
}

.has-danger {
  text-align: left;
  margin-top: 10px;
  margin-left: 20px;
  color: red;
}

.form-danger {
  border: 1px solid red;
}

.option-input {
  -webkit-appearance: none;
  -moz-appearance: none;
  -ms-appearance: none;
  -o-appearance: none;
  appearance: none;

  position: relative;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  height: 20px;
  width: 20px;
  transition: all 0.15s ease-out 0s;
  background: #cbd1d8;
  border: none;
  color: #fff;
  cursor: pointer;
  display: inline-block;
  margin-right: 0.5rem;
  outline: none;
  position: relative;
  z-index: 0;
}

.option-input:disabled,
.option-input:disabled:hover {
  background: #cbd1d8;
  border: 1px solid #cbd1d8;
}

.option-input,
.option-input:checked,
.option-input:hover {
  background: #fff;
  border: 1px solid #039;
}

.option-input:checked::before {
  height: 20px;
  width: 20px;
  position: absolute;
  content: "✔";
  display: inline-block;
  font-size: 16px;
  text-align: center;
  line-height: 20px;
}

.option-input:checked::after {
  background: #fff;
  content: "";

  display: block;
  position: relative;
  z-index: 100;
}

.file-upload-wrapper {
  position: relative;
  width: 100%;
  height: 47px;
  text-align: left;
  padding: 0 20px 0 20px;
  z-index: 0;
}

.file-upload-wrapper input {
  opacity: 0;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  height: 40px;
  margin: 0;
  padding: 0;
  display: block;
  cursor: pointer;
  width: 100%;
}

.file-upload-wrapper:after {
  content: attr(data-text);
  font-size: 18px;
  position: absolute;
  top: 0;
  left: 0;
  background: #fff;
  padding: 22px 15px;
  display: block;
  width: calc(100% - 40px);
  pointer-events: none;
  z-index: 1;
  height: 27px;
  line-height: 27px;
  color: #999;
  border-radius: 30px;
  font-weight: 300;
  border: 1px solid #9e9e9e;
  width: 100%;
}

.file-upload-wrapper:before {
  content: 'Browse';
  position: absolute;
  top: 2px;
  right: 2px;
  display: inline-block;
  height: 42px;
  background: #039;
  color: #fff;
  z-index: 2;
  font-size: 0.876rem;
  line-height: 42px;
  padding: 0 55px;
  text-transform: uppercase;
  pointer-events: none;
  border-radius: 24px;
}

.file-upload-wrapper:hover:before {
  background: #003fbd;
}

.section {
  border-top: 1px solid #999;
  margin: 0 auto;
  width: 40px;
  padding: 20px;
  top: 25px;
  position: relative;
}

.custom-wffm-form [class*='col-'] input {
  padding-left: 20px !important;
}

@media (max-width: 479px) {
  [class*="btn"] {
    width: 100%;
  }

  /* 426px -767px */
  #tracking-snackbar {
    left: 10%;
  }

  .term-con-bottom-mobile {
    display: none;
  }

  .term-con-bottom-pc {
    display: block;
  }

  .span-space-button {
    display: block !important;
  }
}

@media (max-width: 767px) {
  .row-flex {
    display: block;
    flex-wrap: wrap;
  }

  .go-bottom {
    position: fixed;
    bottom: 0px;
    width: 100%;
    left: 0;
  }

  .filelabel {
    font-size: 0.879rem;
  }

  .user-input-wrp .floating-label {
    top: 27px;
    font-size: 0.879rem;
  }

  .file-upload-wrapper:before {
    content: 'Browse';
    position: absolute;
    top: 2px;
    right: 2px;
    display: inline-block;
    height: 42px;
    background: #039;
    color: #fff;
    z-index: 25;
    font-size: 0.768rem;
    line-height: 42px;
    padding: 0 25px;
    text-transform: uppercase;
    pointer-events: none;
    border-radius: 24px;
  }

  /* 426px -767px */
  #tracking-snackbar {
    left: 10%;
  }

  .term-con-bottom-mobile {
    display: none;
  }

  .term-con-bottom-pc {
    display: block;
  }

  .span-space-button {
    width: 30px;
    display: inline-block;
  }
}

@media (min-width: 768px) {

  /* 426px -767px */
  #tracking-snackbar {
    left: 10%;
  }

  .term-con-bottom-mobile {
    display: none;
  }

  .term-con-bottom-pc {
    display: block;
  }

  .span-space-button {
    width: 30px;
    display: inline-block;
  }

  .custom-wffm-form [class*='col-'] input {
    padding-left: 20px !important;
  }
}
</style>
