<template>
  <div class="grid">
    <div class="grid-col_1-11">
      <h1>Выберите жилой комплекс</h1>
    </div>
    <div class="grid-col_1-11 filter-head">
<!--      <div class="filter-buttons">-->
<!--&lt;!&ndash;        <button @click="filter = null" :class="{'no-active': filter !== null}">Все</button>&ndash;&gt;-->
<!--        <button @click="filter = 'Нур-Султан'" :class="{'no-active': filter !== 'Нур-Султан'}">Нур-Султан</button>-->
<!--        <button @click="filter = 'Алматы'" :class="{'no-active': filter !== 'Алматы'}">Алматы</button>-->
<!--      </div>-->
      <div class="certificate-info">
        <img src="~assets/image/gerb.png" alt="" />
        <p>Все указанные ниже проекты имеют <b>сертификат ФГЖС</b></p>
      </div>
    </div>

    <div v-if="inProgressBuilds.length" class="grid-col_1-11">
      <h3 class="build-container-title">В продаже</h3>
      <div  class="build-container">
        <div class="build-box" v-for="item in inProgressBuildsLimit" :key="item.id">
          <img class="build-box__image" :src="item.image" alt="" />
          <h3 class="build-box__title">{{item.title}}</h3>
          <p class="build-box__address">{{item.address}}</p>
          <div class="build-box__info">
            <p class="build-box__area">{{item.area}}</p>
            <p class="build-box__cost">{{item.cost}}</p>
            <p v-if="item.hasOwnProperty('loan')" class="build-box__loan">
            <span
            ><svg
              width="16"
              height="16"
              viewBox="0 0 16 16"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
                <path
                  d="M8 7.5999C12.4187 7.5999 16 6.10615 16 4.26553C16 2.4249 12.4187 0.931152 8 0.931152C3.58125 0.931152 0 2.4249 0 4.26553C0 6.10615 3.58125 7.5999 8 7.5999ZM8 12.9312C4.94688 12.9312 2.24688 12.1968 0.54375 11.0624C0.196875 11.4374 0 11.8405 0 12.2655C0 14.1062 3.58125 15.5999 8 15.5999C12.4187 15.5999 16 14.1062 16 12.2655C16 11.8405 15.8031 11.4374 15.4563 11.0655C13.7531 12.1968 11.0531 12.9312 8 12.9312ZM8 8.93115C4.94688 8.93115 2.24688 8.19678 0.54375 7.0624C0.196875 7.4374 0 7.84053 0 8.26553C0 10.1062 3.58125 11.5999 8 11.5999C12.4187 11.5999 16 10.1062 16 8.26553C16 7.84053 15.8031 7.4374 15.4563 7.06553C13.7531 8.19678 11.0531 8.93115 8 8.93115Z"
                  fill="#FFA621"
                />
              </svg>
            </span>
              {{item.loan}}
            </p>
          </div>
          <a v-if="item.link" :href="item.link" target="_blank" class="build-box__link"
          >Узнать подробнее
            <svg
              width="5"
              height="12"
              viewBox="0 0 5 12"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                clip-rule="evenodd"
                d="M3.49112 8L0.183058 4.97549C-0.0610197 4.75233 -0.0610198 4.39052 0.183058 4.16737C0.427136 3.94421 0.822864 3.94421 1.06694 4.16737L4.81694 7.59594C5.06102 7.8191 5.06102 8.1809 4.81694 8.40406L1.06694 11.8326C0.822864 12.0558 0.427136 12.0558 0.183058 11.8326C-0.0610194 11.6095 -0.0610195 11.2477 0.183058 11.0245L3.49112 8Z"
                fill="#004B94"
              />
            </svg>
          </a>
        </div>
      </div>
      <div v-if="inProgressBuilds.length > viewLimitProgress" class="view-more">
        <button @click="viewLimitProgress += 6">Показать больше проектов</button>
      </div>
    </div>
    <div v-if="perspectiveBuilds.length" class="grid-col_1-11">
      <h3 class="build-container-title">Перспективные с ФГЖС</h3>
      <div class="build-container">
        <div class="build-box" v-for="item in perspectiveBuildsLimit" :key="item.id">
          <img class="build-box__image" :src="item.image" alt="" />
          <h3 class="build-box__title">{{item.title}}</h3>
          <p class="build-box__address">{{item.address}}</p>
          <div class="build-box__info">
            <p class="build-box__area">{{item.area}}</p>
            <p class="build-box__cost">{{item.cost}}</p>
            <p v-if="item.hasOwnProperty('loan')"  class="build-box__loan">
            <span
            ><svg
              width="16"
              height="16"
              viewBox="0 0 16 16"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
                <path
                  d="M8 7.5999C12.4187 7.5999 16 6.10615 16 4.26553C16 2.4249 12.4187 0.931152 8 0.931152C3.58125 0.931152 0 2.4249 0 4.26553C0 6.10615 3.58125 7.5999 8 7.5999ZM8 12.9312C4.94688 12.9312 2.24688 12.1968 0.54375 11.0624C0.196875 11.4374 0 11.8405 0 12.2655C0 14.1062 3.58125 15.5999 8 15.5999C12.4187 15.5999 16 14.1062 16 12.2655C16 11.8405 15.8031 11.4374 15.4563 11.0655C13.7531 12.1968 11.0531 12.9312 8 12.9312ZM8 8.93115C4.94688 8.93115 2.24688 8.19678 0.54375 7.0624C0.196875 7.4374 0 7.84053 0 8.26553C0 10.1062 3.58125 11.5999 8 11.5999C12.4187 11.5999 16 10.1062 16 8.26553C16 7.84053 15.8031 7.4374 15.4563 7.06553C13.7531 8.19678 11.0531 8.93115 8 8.93115Z"
                  fill="#FFA621"
                />
              </svg>
            </span>
              {{item.loan}}
            </p>
          </div>
          <a v-if="item.link" :href="item.link" class="build-box__link"
          >Узнать подробнее
            <svg
              width="5"
              height="12"
              viewBox="0 0 5 12"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                clip-rule="evenodd"
                d="M3.49112 8L0.183058 4.97549C-0.0610197 4.75233 -0.0610198 4.39052 0.183058 4.16737C0.427136 3.94421 0.822864 3.94421 1.06694 4.16737L4.81694 7.59594C5.06102 7.8191 5.06102 8.1809 4.81694 8.40406L1.06694 11.8326C0.822864 12.0558 0.427136 12.0558 0.183058 11.8326C-0.0610194 11.6095 -0.0610195 11.2477 0.183058 11.0245L3.49112 8Z"
                fill="#004B94"
              />
            </svg>
          </a>
        </div>
      </div>
      <div v-if="perspectiveBuilds.length > viewLimitPerspective" class="view-more">
        <button @click="viewLimitPerspective += 6">Показать больше проектов</button>
      </div>
    </div>

    <div class="grid-col_1-11 view-more">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M12 20C14.1217 20 16.1566 19.1571 17.6569 17.6569C19.1571 16.1566 20 14.1217 20 12C20 9.87827 19.1571 7.84344 17.6569 6.34315C16.1566 4.84285 14.1217 4 12 4C9.87827 4 7.84344 4.84285 6.34315 6.34315C4.84285 7.84344 4 9.87827 4 12C4 14.1217 4.84285 16.1566 6.34315 17.6569C7.84344 19.1571 9.87827 20 12 20ZM12 22C6.477 22 2 17.523 2 12C2 6.477 6.477 2 12 2C17.523 2 22 6.477 22 12C22 17.523 17.523 22 12 22ZM11 11V17H13V11H11ZM11 7H13V9H11V7Z" fill="#4F4F4F"/>
      </svg>

      <p> Данное предложение распространяется только на жилые комплексы имеющие сертификат ФГЖС</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'select-build',
  props: ['selectBuilds'],
  data: () => ({
    filter: 'Нур-Султан',
    viewLimitProgress: 6,
    viewLimitPerspective: 6
  }),
  computed: {
    selectBuildsFilter(){
      return this.selectBuilds
    },
    inProgressBuilds(){
      return this.selectBuildsFilter.filter(item => item.status === 'inProgress')
    },
    inProgressBuildsLimit(){
      return this.inProgressBuilds.slice(0, this.viewLimitProgress)
    },
    perspectiveBuilds(){
      return this.selectBuildsFilter.filter(item => item.status === 'perspective')
    },
    perspectiveBuildsLimit(){
      return this.perspectiveBuilds.slice(0, this.viewLimitPerspective)
    }
    // selectBuildLimit(){
    //   return this.selectBuildsFilter.slice(0, this.viewLimit)
    // },

  }
}
</script>

<style lang="scss" scoped>
.filter-head {
  display: flex;
  justify-content: flex-end;
  align-items: center;

  .filter-buttons {
    display: grid;
    grid-template-columns: repeat(3, auto);
    gap: 1.6rem;
    button {
      padding: 7px 1.6rem;
      font-size: 1.8rem;
      &.no-active{
        background-color: white;
        color: #333333;
        &:hover{
          color: #004b94;
          background-color: #FFEFE2;
        }
      }

    }
  }
  .certificate-info {
    display: flex;
    align-items: center;
    color: #7a1435;
    img {
      margin-right: 8px;
    }
  }
  @media screen and (max-width: 768px) {
    flex-direction: column-reverse;
    align-items: flex-start;
    .filter-buttons {
      gap: 1rem;
      button{
        font-size: 1.6rem;
      }
    }
    .certificate-info {
      margin-bottom: 2.4rem;
    }
  }
}

.build-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 3.2rem;
  grid-row-gap: 5.4rem;
  .build-box {
    &__image {
      width: 100%;
      height: 344px;
      object-fit: cover;
      margin-bottom: 1.6rem;
      border-radius: 8px;
    }
    &__title {
      color: #BE6C2F;
      margin-bottom: 6px;
    }
    &__address {
      margin-bottom: 6px;
      font-weight: 600;
    }
    &__info {
      display: grid;
      grid-template-columns: repeat(3, auto);
      gap: 1.2rem;
      margin-bottom: 1.2rem;
      color: #828282;
    }
    &__loan {
      color: #f19710;
      font-weight: bold;
      display: flex;
      align-items: center;
      svg {
        margin-right: 4px;
      }
    }
    &__link {
      display: flex;
      align-items: center;
      color: #BE6C2F;
      svg {
        margin-left: 6px;
      }
      &:hover{
        text-decoration: underline;
      }
    }
  }
  @media screen and (max-width: 1024px) {
    .build-box{
      &__image {
        height: 280px;

      }
    }
  }
  @media screen and (max-width: 900px) {
    grid-template-columns: repeat(2, 1fr);
  }
  @media screen and (max-width: 768px) {
    grid-template-columns: repeat(1, 1fr);
    max-width: 400px;
    margin: auto;
    .build-box {
      &__info {
        grid-template-columns: repeat(2, auto);
      }
    }
  }
}
.build-container-title{
  font-weight: 600;
  font-size: 28px;
  line-height: 32px;
  color: #1E1F21;
  margin-bottom: 3.2rem;
}
.view-more{
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 4rem;
  svg{
    margin-right: 1.2rem;
  }
  button{
      width: 100%;
    max-width: 30rem;
  }
}
</style>
