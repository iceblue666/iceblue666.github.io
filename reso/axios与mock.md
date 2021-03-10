\-\-\-
title:axios与mock
time:2021-03-09 17:27:00
categories:总结
tags:axios,mock,前端
summary:日常总结知识
\-\-\-
# axios与mock

## 1. post用法

```
      this.$axios.post('/TitleById',{
        id : this.$route.params.id
      }).then(res => {
        this.list = list.concat(arr);
        if(this.$route.name === 'Article'){
          this.list.push({meta:{breadNav:res.data.data.title,name:null}})
        }
      }).catch(err => {
        console.log(err);
      })
```

```
export default {
  'post|/articleDetail': option => {
    return {
      status: 200,
      message: 'success',
      data: extractDataByArr([JSON.parse(option.body).id])
    };
  }
}
```

