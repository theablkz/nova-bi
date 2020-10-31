<template>
  <div class="grid">
    <div class="grid-col_1-6">
      <div class="indent_bottom-h2">
        <h1>Ежемесячный платеж по ипотеке</h1>
        <p style="font-size: 18px;">На примере типовой планировки</p>
      </div>
      <div class="filter-block">
        <div class="desktop_none">
          <label for="room" >
            <select v-model="rooms" name="room" id="room">
              <option v-for="(item, index) in builds" :value="index">
                {{ item.text }}
              </option>
            </select>
          </label>
        </div>
        <div
          class="custom-select mobile_none"
          :class="{ 'custom-select--active': roomsSelect }"
        >
          <p @click="roomsSelect = !roomsSelect" class="custom-select__value">
            {{ builds[rooms].text }}
            <span
              ><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<path d="M12.0013 16C11.7676 16.0005 11.5412 15.9191 11.3613 15.77L5.36125 10.77C5.15704 10.6003 5.02861 10.3564 5.00423 10.0919C4.97985 9.8275 5.06151 9.56422 5.23125 9.36C5.40099 9.15578 5.6449 9.02736 5.90933 9.00298C6.17375 8.9786 6.43704 9.06026 6.64125 9.23L12.0013 13.71L17.3613 9.39C17.4635 9.30694 17.5812 9.2449 17.7076 9.20747C17.8339 9.17004 17.9664 9.15795 18.0974 9.17189C18.2285 9.18582 18.3554 9.22552 18.4711 9.2887C18.5867 9.35187 18.6887 9.43727 18.7713 9.54C18.8628 9.64282 18.9322 9.76345 18.975 9.89432C19.0178 10.0252 19.0331 10.1635 19.0199 10.3006C19.0068 10.4376 18.9655 10.5705 18.8986 10.6909C18.8317 10.8112 18.7407 10.9165 18.6313 11L12.6313 15.83C12.4462 15.9555 12.2244 16.0154 12.0013 16Z" fill="#BE6C2F"/>
</svg>

            </span>
          </p>
          <div v-if="roomsSelect" class="custom-select__options-box">
            <p
              v-for="(item, index) in builds"
              @click="
                () => {
                  rooms = index
                  roomsSelect = false
                }
              "
            >
              {{ item.text }}
            </p>
          </div>
        </div>
        <p style="margin: 1rem; font-size: 22px; font-weight: 500;">квартира в ЖК</p>
        <p style="margin: 1rem; font-size: 22px; font-weight: 500;">{{builds[rooms].values.buildName}}</p>
<!--        <div class="desktop_none">-->
<!--          <label  for="build">-->
<!--            <select v-model="build" name="build" id="build">-->
<!--              <option v-for="item in builds[rooms].values" :value="item">-->
<!--                {{ item.buildName }}-->
<!--              </option>-->
<!--            </select>-->
<!--          </label>-->
<!--        </div>-->
<!--        <div-->
<!--          class="custom-select mobile_none"-->
<!--          :class="{ 'custom-select&#45;&#45;active': buildSelect }"-->
<!--        >-->
<!--          <p @click="buildSelect = !buildSelect" class="custom-select__value">-->
<!--            {{ build.buildName }}-->
<!--            <span-->
<!--            ><svg-->
<!--              width="24"-->
<!--              height="24"-->
<!--              viewBox="0 0 24 24"-->
<!--              fill="none"-->
<!--              xmlns="http://www.w3.org/2000/svg"-->
<!--            >-->
<!--                <path-->
<!--                  d="M12 16C11.7663 16.0005 11.5399 15.9191 11.36 15.77L5.35997 10.77C5.15575 10.6003 5.02733 10.3564 5.00295 10.092C4.97857 9.82753 5.06023 9.56425 5.22997 9.36003C5.39971 9.15581 5.64362 9.02739 5.90805 9.00301C6.17247 8.97863 6.43575 9.06029 6.63997 9.23003L12 13.71L17.36 9.39003C17.4623 9.30697 17.58 9.24493 17.7063 9.2075C17.8326 9.17007 17.9651 9.15798 18.0962 9.17192C18.2272 9.18586 18.3542 9.22555 18.4698 9.28873C18.5854 9.3519 18.6874 9.4373 18.77 9.54003C18.8616 9.64285 18.9309 9.76348 18.9737 9.89435C19.0165 10.0252 19.0318 10.1635 19.0187 10.3006C19.0055 10.4377 18.9642 10.5705 18.8973 10.6909C18.8304 10.8112 18.7394 10.9165 18.63 11L12.63 15.83C12.4449 15.9555 12.2231 16.0154 12 16Z"-->
<!--                  fill="#004B94"-->
<!--                />-->
<!--              </svg>-->
<!--            </span>-->
<!--          </p>-->
<!--          <div v-if="buildSelect" class="custom-select__options-box">-->
<!--            <p-->
<!--            >-->
<!--              {{ builds[rooms].values.buildName }}-->
<!--            </p>-->
<!--          </div>-->
<!--        </div>-->
      </div>

      <div class="build-detail">
        <div class="build-detail__columns indent_bottom-h4">
          <div>
            <h2>{{ build.cost }}</h2>
            <p>Стоимость за квартиру</p>
          </div>
          <div>
            <h2>{{ build.payment }}</h2>
            <p>Ежемесячный платеж</p>
          </div>
        </div>
        <div class="build-detail__columns">
          <p>Площадь</p>
          <p class="bold">{{ build.area }}</p>
        </div>
        <div class="build-detail__columns">
          <p>Первоначальный взнос</p>
          <p class="bold">{{ build.anInitialFee }}</p>
        </div>
        <div class="build-detail__columns">
          <p>Срок займа</p>
          <p class="bold">{{ build.loanTerm }}</p>
        </div>
        <div class="build-detail__columns">
          <p>Ставка</p>
          <p class="bold">{{ build.rate }}</p>
        </div>
      </div>
    </div>
    <div class="grid-col_6-11" style="align-self: center">
      <img class="scheme" :src="build.scheme" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'calculateMortgage',
  props: ['builds'],
  data() {
    const roomsIndex = 0
    return {
      rooms: roomsIndex,
      build: this.builds[roomsIndex].values,
      roomsSelect: false,
      buildSelect: false
    }
  },
  watch: {
    rooms: function (a) {
      this.build = this.builds[a].values
    },
  },
}
</script>

<style lang="scss" scoped>
.custom-select {
  position: relative;
  user-select: none;
  &__value {
    color: #BE6C2F;
    border-bottom: 1px dashed #BE6C2F;
    font-weight: 500;
    font-size: 22px;
    cursor: pointer;
    padding-bottom: 0.4rem;
    display: flex;
    align-items: center;
    border-radius: 8px 8px 0 0;
    padding: .8rem 1rem;
    &:hover{
      background-color: #FFEFE2;
    }
  }
  &__options-box {
    position: absolute;
    z-index: 5;
    top: 100%;
    left: 0;
    right: 0;
    background-color: white;
    box-shadow: 0px 4px 70px rgba(22, 55, 69, 0.15);
    padding: 1.4rem 0;
    p {
      font-weight: 500;
      font-size: 18px;
      padding: 0.8rem 0;
      cursor: pointer;
      &:hover {
        color: #BE6C2F;
        background-color: #FFEFE2;
      }
    }
  }
  &--active {
    svg{
      transition: transform .3s ease;
      transform: rotate(180deg);
    }
  }
}
.filter-block {
  display: flex;
  flex-wrap: wrap;
  text-align: center;
  align-items: center;
  margin-bottom: 2.2rem;
  color: #01152c;
  font-weight: 500;
  font-size: 20px;
  label {
    position: relative;
    display: flex;
    cursor: pointer;

    select {
      font-weight: 500;
      font-size: 20px;
      background-color: inherit;
      border-radius: 0;
      color: #004b94;
      border: none;
      padding: 0;
      min-height: auto;
      border-bottom: 1px #004b94 dashed;
      -webkit-appearance: none;
      -moz-appearance: none;
      appearance: none;
      option {
        padding: 1rem;
        border-radius: 8px;
      }
    }
    &:after {
      content: '';
      display: block;
      background-image: url('~assets/image/icons/arrow-down.svg');
      background-size: 28px 28px;
      height: 28px;
      width: 28px;
    }
  }
  @media screen and (max-width: 768px){
    grid-template-columns: auto 1fr;
    gap: 2rem;
    font-size: 2.2rem;
    label {
      select {
        font-size: 2.2rem;
      }
    }
  }
}
.build-detail {
  padding: 32px 25px;
  background: #ffffff;
  box-shadow: 0px 4px 70px rgba(22, 55, 69, 0.15);
  border-radius: 16px;
  display: grid;
  grid-row-gap: 12px;
  p {
    font-size: 1.6rem;
  }
  h2 {
    color: #128c7e;
  }
  &__columns {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 4rem;
  }
  @media (max-width: 768px){
    padding: 32px 16px;
    margin: 0 -16px;
  }
}
.scheme {
  width: 100%;
  object-fit: contain;
  margin: auto;
  @media (max-width: 768px){
  }
}
</style>
