<template>
<div class="card " :class="{'card-outline-success': message.isFirst}">
  <div class="card-block">
    <h5 class="card-title">{{ message.title }}</h5>
    <p class="card-text">{{ message.text }}</p>
    <p class="card-text">
      <small class="text-muted">Added on 
       {{ message.timestamp | formatDate}}
      </small>
    </p>
  </div>
</div>
</template>
<script>
import moment from 'moment';
export default {
  props: ['message'],
  filters: {  
    formatDate(time) {  
      return time ? moment(time).format('MMMM Do YYYY, h:mm:ss a') : '';
    }  
  }  
};
</script>
<style scoped>
.card-outline-success {
    border-color: #5cb85c;
}
</style>

