<template>
  <form v-if="!registrationPassed" class="sign-up form" @submit.prevent="checkForm">
    <div class="form-group required">
      <label for="surname">Фамилия:</label>
      <input
        id="surname"
        class="form-control"
        :class="$v.form.surname.$error ? 'is-invalid' : ''"
        v-model.trim="form.surname">
      <p v-if="$v.form.surname.$dirty && !$v.form.surname.required" class="invalid-feedback">
        Обязательное поле
      </p>
      <p v-if="$v.form.surname.$dirty && !$v.form.surname.alpha" class="invalid-feedback">
        Поле может состоять только из кирилицы
      </p>
    </div>
    <div class="form-group required">
      <label for="firstName">Имя:</label>
      <input
        id="firstName"
        class="form-control"
        :class="$v.form.firstName.$error ? 'is-invalid' : ''"
        v-model.trim="form.firstName">
      <p v-if="$v.form.firstName.$dirty && !$v.form.firstName.required" class="invalid-feedback">
        Обязательное поле
      </p>
      <p v-if="$v.form.firstName.$dirty && !$v.form.firstName.alpha" class="invalid-feedback">
        Поле может состоять только из кирилицы
      </p>
    </div>
    <div class="form-group">
      <label for="patronymic">Отчество:</label>
      <input
        id="patronymic"
        class="form-control"
       v-model.trim="form.patronymic">
    </div>
    <div class="form-group required">
      <label for="birthday">Дата рождения:</label>
      <input
      id="birthday"
      type="date"
      class="form-control"
      :class="$v.form.birthday.$error ? 'is-invalid' : ''"
      v-model.trim="form.birthday">
      <p v-if="$v.form.birthday.$dirty && !$v.form.birthday.required" class="invalid-feedback">
        Обязательное поле
      </p>
    </div>
    <div class="form-group required">
      <label for="tel">Номер телефона:</label>
      <input
      id="tel"
      class="form-control"
      :class="$v.form.tel.$error ? 'is-invalid' : ''"
      v-model.trim="form.tel">
      <p v-if="$v.form.tel.$dirty && !$v.form.tel.alpha" class="invalid-feedback">
        поле должно состоять из 11 цифр и начинаться с 7
      </p>
    </div>
    <div class="radio-group">
      <div class="form-check">
        <input type="radio" value="male" name="exampleRadios" id="male" v-model="form.gendere" >
        <label class="label" for="male">
          Мужчина
        </label>
      </div>
      <div class="form-check">
        <input class="ml-20" type="radio" value="female" name="exampleRadios" id="female" v-model="form.gendere">
        <label class="label" for="female">
          Женщина
        </label>
      </div>
    </div>
    <div class="select-group">
      <label for="doctor" class="label">Лечащий врач:</label>
      <select id="doctor" 
      class="select"
      v-model="form.doctor">
        <option
        v-for="(doctor, index) of doctors"
        :key="index"
        :value="doctor.value">
          {{doctor.label}}
        </option>
      </select>
    </div>
    <div class="select-group required">
      <label for="group" class="label">Группа клиентов:</label>
      <select id="group" 
      class="select"
      :class="$v.form.favorite.$error ? 'is-invalid' : ''"
      v-model="form.favorite"
      multiple>
        <option
        v-for="(group, index) of groups"
        :key="index"
        :value="group.value">
          {{group.label}}
        </option>
      </select>
      <p v-if="$v.form.favorite.$dirty && !$v.form.favorite.required" class="invalid-feedback">
        Обязательное поле
      </p>
    </div>
    <div class="checkbox-group">
      <input type="checkbox"  
      id="notification" 
      v-model="form.agreeWithSendSms">
      <label class="label" for="notification">Не отправлять СМС</label>
    </div>
    <div class="form-group">
      <label for="zip">Индекс:</label>
      <input
      id="zip"
      class="form-control"
      v-model.trim="form.zip">
    </div>
    <div class="form-group">
      <label for="country">Страна:</label>
      <input
      id="country"
      class="form-control"
      v-model.trim="form.country">
    </div>
    <div class="form-group">
      <label for="region">Область:</label>
      <input
      id="region"
      class="form-control"
      v-model.trim="form.region">
    </div>
    <div class="form-group required">
      <label for="city">Город:</label>
      <input
      id="city"
      class="form-control"
      :class="$v.form.city.$error ? 'is-invalid' : ''"
      v-model.trim="form.city">
      <p v-if="$v.form.city.$dirty && !$v.form.city.required" class="invalid-feedback">
        Обязательное поле
      </p>
    </div>
    <div class="form-group">
      <label for="street">Улица:</label>
      <input
      id="street"
      class="form-control"
      v-model.trim="form.street">
    </div>
    <div class="form-group">
      <label for="house">Дом:</label>
      <input
      id="house"
      class="form-control"
      v-model.trim="form.house">
    </div>
    <div class="select-group required mt-30 mb-0">
      <label for="doc" class="label">Тип документа:</label>
      <select id="doc" 
      class="select"
      v-model="form.doc">
        <option
        v-for="(doc, index) of documents"
        :key="index"
        :value="doc.value">
          {{doc.label}}
        </option>
      </select>
    </div>
    <div class="form-group">
      <label for="series">Серия:</label>
      <input
      id="series"
      class="form-control"
      v-model.trim="form.series">
    </div>
    <div class="form-group">
      <label for="number">Номер:</label>
      <input
      id="number"
      class="form-control"
      v-model.trim="form.number">
    </div>
    <div class="form-group">
      <label for="issuance">Кем выдан:</label>
      <input
      id="issuance"
      class="form-control"
      v-model.trim="form.issuance">
    </div>
    <div class="form-group required">
      <label for="issueDate">Дата выдачи:</label>
      <input
      id="issueDate"
      type="date"
      :class="$v.form.issueDate.$error ? 'is-invalid' : ''"
      v-model.trim="form.issueDate">
      <p v-if="$v.form.issueDate.$dirty && !$v.form.issueDate.required" class="invalid-feedback">
        Обязательное поле
      </p>
    </div>
    <button type="submit" class="btn">Сохранить</button>
  </form>
      <div v-else>
      <h1>
        {{ `${ form.surname }, успешно зарегистрирован!` }}
      </h1>
    </div>

</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, alpha, numeric, maxLength } from 'vuelidate/lib/validators'
export default {
  mixins: [validationMixin],
  data() {
    return {
      registrationPassed: false,
      form:{
        surname: '',
        firstName: '',
        patronymic: '',
        birthday: '',
        tel: '',
        doctor: 'Ivanov',
        favorite: [''],
        agreeWithSendSms: false,
        gendere: 'male',
        zip: '',
        country: 'Россия',
        region: '',
        city: '',
        street: '',
        house: '',
        doc: 'passport',
        issueDate: '',
        issuance: '',
        number: '',
        series: ''
      },
      doctors: [
        {
          label: 'Иванов',
        value: 'Ivanov'
        },
        {
          label: 'Захаров',
        value: 'Zakharov'
        },
        {
          label: 'Чернышева',
        value: 'Chernysheva'
        }
      ],
      groups: [
        {
          label: 'VIP',
        value: 'VIP'
        },
        {
          label: 'Проблемные',
        value: 'problems'
        },
        {
          label: 'ОМС',
        value: 'OMS'
        }
      ],
    documents: [
        {
          label: 'Паспорт',
        value: 'passport'
        },
        {
          label: 'Свидетельство о рождении',
        value: 'birthСertificate'
        },
        {
          label: 'Вод. удостоверение',
        value: 'driverLicense'
        }
      ]
    }
  },
  validations: {
    form: {
      surname: {required, alpha: val => /^[а-яё]*$/i.test(val)},
      firstName: {required, alpha: val => /^[а-яё]*$/i.test(val)},
      birthday: {required},
      tel: {required, minLength: minLength(11), maxLength: maxLength(11), alpha: val => /7[0-9]{10}/.test(val)},
      favorite: {required},
      city:{required},
      doc: {required},
      issueDate: {required}
    }
  },
  methods: {
    checkForm() {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        this.registrationPassed = true
      }
    }
  }
}
</script>

<style scoped>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    .form {
      margin: 20px auto 50px;
      max-width: 400px;
      padding: 10px;
    }

    .form-group {
      margin: 0 0 20px;
      position: relative;
      height: 65px;
    }

    .form-group label {
      margin-bottom: 10px;
      display: inline-block;
    }

    .form-group input {
      width: 100%;
      height: 40px;
      border-radius: 3px;
      padding: 5px;
    }

    .radio-group,
    .select-group,
    .checkbox-group {
      margin: 0 0 20px;
      position: relative;
      min-height: 40px;
      display: flex;
      align-items: flex-start;
    }
    .radio-group .label,
    .checkbox-group .label {
      margin-left: 10px;
      position: relative;
    }
    .select-group .label {
      position: relative;
      margin-right: 10px;
      padding: 5px 0
    }

    .select {
      height: 30px;
      width: 150px;
      border: 1px solid #000;
      background: transparent;
      border-radius: 5px;
      flex-grow: 1;
    }

    .select[multiple] {
      height: 80px;
    }

    .select[multiple] option {
      padding: 5px;
    }

    .ml-20 {
      margin-left: 20px;
    }

    .mb-0 {
      margin-bottom: 0;
    }

    .mt-30 {
      margin-top: 30px;
    }

    .required label {
      position: relative;
    }
    .required label::after {
      content: '*';
      display: block;
      position: absolute;
      width: 5px;
      height: 5px;
      border-radius: 50%;
      color: red;
      top: 0;
      right: -7px;
    }
    .btn {
      padding: 10px 20px;
      background:rgb(0 117 255);
      color: white;
      border: none;
      border-radius: 3px;
    }
    .is-invalid {
      border: 2px solid red;
    }
    .invalid-feedback {
      color: tomato;
    }
</style>