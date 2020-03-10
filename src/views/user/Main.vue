<template>
    <div class="main-content">
        <div class="profile-content">
            <div class="profile-avatar">
                <a class="p-photo p-block" href="#">
                    <img width="260" height="260" class="p-avatar" src="https://avatars1.githubusercontent.com/u/46558390?s=460&v=4">
                </a>
            </div>
            <div class="profile-clear">
                <h1 class="profile-names">
                    <span class="p-name p-block">木子</span>
                    <span class="p-signature p-block">念旧的人活的像个拾荒者，不动声色，却满心澎湃</span>
                </h1>
            </div>
        </div>
        <div class="content-list">
            
        </div>
    </div>
</template>
<script>
export default {
  name: "login",
  data() {
    return {
         
    }
  },
  
   
  methods: {
  }
    
}
</script>
<style> 
.main-conte{
    min-width: 500px;
}
.profile-content{
    padding-right: 16px!important;
    padding-left: 16px!important;
    margin-top:24px!important ;
}
.profile-avatar{
    width: 25%;
    float: left!important;
    padding-right: 16px!important;
   
}
a{
    color: #0366d6;
    text-decoration: none;
    
}
.p-photo{

}
.p-avatar{
    width: 100%!important;
    height: 100%!important;
    line-height: 1;
    vertical-align: middle;
    border-radius: 3px;
}
.p-block{
    display: block!important;
}
.profile-clear{
    padding-bottom: 4px!important;
    padding-top: 4px!important;
    float: left!important;
    
}
h1{
    font-weight: 600;
    font-size: 32px;
    margin-top: 0;
    margin-bottom: 0;
}
.p-name{
    font-size: 26px;
    line-height: 30px;
    overflow: hidden!important;
}
.p-signature{
    font-size: 15px;
    font-style: normal;
    font-weight: 300;
    line-height: 24px;
    color: #666;
}
</style>