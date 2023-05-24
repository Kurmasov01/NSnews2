<template>
    <Page>
      <ScrollView>
        <StackLayout class="news-container">
          <TextField v-model="searchQuery" hint="Введите запрос"/>
          <Label/>

          <Label text="Введите дату в формате ГГГГ-ММ-ДД"/>
          <TextField v-model="selectFrom" hint="От" />
          <TextField v-model="selectTo" hint="До" />
          <Button text="Найти новости" @tap="fetchNews" class="btn"/>
          <Label/>
          <StackLayout v-for="newsItem in newsItems" :key="newsItem.title" class="news-card">
            
            <Image :src="newsItem.image" stretch="aspectFill" height="200" />
            <Label :text="newsItem.title" class="title" textWrap="true" />
            <Label :text="newsItem.description" textWrap="true" />
            <Label :text="newsItem.publishedAt.slice(0, -10)" />
            <Label/>

          </StackLayout>
        </StackLayout>
      </ScrollView>
    </Page>
  </template>
  
  <script>
  export default {
    data() {
      return {
        selectFrom: "",
        selectTo: "",
        searchQuery: "",
        newsItems: [
  
          
        ],
        test: ""
      };
    },
    methods: {
      fetchNews() {
        fetch(`https://gnews.io/api/v4/search?q=${this.searchQuery}&apikey=69efc8edf320ba963b6f92942d88039d&lang=ru&from=${this.selectFrom}T12:00:00Z&to=${this.selectTo}T12:00:00Z`)
          .then(response => response.json())
          .then(data => {
            this.newsItems = data.articles;
          })
          .catch(error => {
            console.error('Ошибка при получении новостей:', error);
            console.log('Ошибка при получении новостей:', error);
          });
      },
    }
  };
  </script>
  
  <style scoped>
  .news-container {
    padding: 16px;
  }
  
  .news-card {
    background-color: #ffffff;
    border-radius: 8px;
    margin-bottom: 16px;
    padding: 16px;
  }
  .title {
    font-weight: bold;
    font-size: 18px;
    margin-bottom: 8px;
  }
  .btn {
    background-color: rgb(0, 191, 216);
  }
  </style>