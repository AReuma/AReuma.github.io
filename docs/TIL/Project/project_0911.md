---
layout: default
title: 23.09.11 TIL
parent: TIL
---

# 23.09.11 TIL
## Tiptap과 Aws S3 구현  
    
>🗓️ 날짜 : 2023.09.09   
> 📚 할 일 : 개인 프로젝트 진행, 블로그 작성   
> 📝오늘의 목표:  [SELLMS], [SELLP]진행, redis 적용   
> ⌛ 공부시간 : 9:00 ~


## 1. Tiptap 라이브러리 이용  

지금까지 진행한 프로젝트는 글 안에 이미지를 넣는 게 아니라 먼저 넣은 이미지가 다 보이고 그 밑으로 내용이 보이도록 구현했다.
이번 프로젝트에서는 내용 안에 원하는 이미지를 넣어서 볼 수 있도록 구현하고 싶었다.
  
인터넷으로 찾아보니 Tiptap이라는 라이브러리를 이용하면 원하는 대로 구현할 수 있었다.

[https://tiptap.dev/](https://tiptap.dev/)
  
![tiptap-editor.png](/assets/images/TIL/project/0911/tiptap-editor.png)  

tiptab 홈페이지 문서를 따라서 작성하니 글을 작성하는 건 구현이 완료되었으나 사진을 중간마다 넣을 방법을 몰랐다. 
  
[https://tiptap.dev/api/nodes/image](https://tiptap.dev/api/nodes/image)  
이 페이지를 따라서 실행하면 이미지 URL을 넣으면 사진이 글 상자 안으로 넣을 수 있었다.
하지만 내가 원하는 건 이미지를 내 컴퓨터에서 가지고 오는 방법이었다.  


구글에 여러 가지 키워드로 검색하고 챗 GPT에 물어도 봤지만 제대로 구현이 되지 않았다.

[How to upload images with Tiptap editor](https://gist.github.com/slava-vishnyakov/16076dff1a77ddaca93c4bccd4ec4521)    
[Adding drag and drop image uploads to Tiptap](https://www.codemzy.com/blog/tiptap-drag-drop-image)  
  
  
## 1) 처음 시도한 코드 구현  
tiptab 라이브러리에는 이미지 URL을 알면 올릴 수 있는데 file로 열면 가져올 수 있지 않을까? 하는 생각이 들어 구현했다.   

```html
 <div>
    <input type="file" @change="handleFileUpload">
    <button @click="uploadFile">파일 업로드</button>
</div>
```

```vue
<script>
export default {
  data() {
    return {
      selectedFile: null,
      previewURL: null
    };
  },
  methods: {
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.previewURL = e.target.result;
        };
        reader.readAsDataURL(file);
        this.selectedFile = file;
      }
    },
    uploadFile() {
      let formData = new FormData();
      formData.append('file', this.selectedFile);

    },
  },
};
</script>
```
`previewURL`은 DataURL 형식으로 읽어오니깐 똑같은 게 아닌가 하는 생각에 시도했다.  

### 1️⃣ DataURL
    * 형식: data:image/png;base64,iVBORw0KGg...  
    * 이미지 파일 전체를 문자열로 표현

### 2️⃣ 이미지 URL  
    * 형식: 'https://example.com/images/example.jpg'
    * 이미지 파일이 위치한 경로  
  
<hr/>   
  

이제 포기할까 하는 시점에 큰 힌트를 준 코드를 발견했다.  

[https://codesandbox.io/s/1tswk?file=/src/components/Editor.vue:2870-2894](https://codesandbox.io/s/1tswk?file=/src/components/Editor.vue:2870-2894)
  
```vue
fileChange(e) {
      const file = this.$refs.file.files[0];
      const uploadUrl = `https://httpbin.org/post`;
      let formData = new FormData();

      formData.append("file", this.file);

      console.log("Uploading...");

      axios.post(uploadUrl).then(data => {
        // Take the URL/Base64 from `data` returned from server
        alert("Your image has been uploaded to the server");
        alert("NOTE THIS IS A DUMMY DEMO, THERE IS NO BACKEND");

        this.imageSrc = "https://source.unsplash.com/random/400x100";
      });
    },
    insertImage() {
      const data = {
        command: this.command,
        data: {
          src: this.imageSrc
          // alt: "YOU CAN ADD ALT",
          // title: "YOU CAN ADD TITLE"
        }
      };

      this.$emit("onConfirm", data);
      this.closeModal();
    },

```  
Take the URL/Base64 from `data` returned from server
서버에서 반환된 URL/Base64를 가져온다는 문장을 보고 직접 클라우드에 올리고 content 안으로 넣으면 되겠다는 생각이 들었다.
  
  
> Spring boot과 AWS s3를 연동시키고, 이미지를 업로드 누르면 AWS s3에 저장이 되도록 구현했다.
  
그러면 여기서 문제점은 판매자가 선택한 사진은 이미 클라우드에 올라가 있는 상태도 작성하다가 사진이 필요가 없어서 지우게 된다면, 필요 없는 데이터만 쌓이게 되는 것이다.
  
  
이 해결 방법은 선택한 이미지의 이름을 배열로 갖고 있다가 판매자가 글을 작성하고 저장을 누를 때 이미지의 이름들을 백으로 넘겨서 있는지 확인하고 없으면 지우도록 구현할 예정이다.
  
![uploadImg1.png](/assets/images/TIL/project/0911/uploadImg1.png)  

![uploadImg2.png](/assets/images/TIL/project/0911/uploadImg2.png)   
  

![uploadImg3.png](/assets/images/TIL/project/0911/uploadImg3.png)
  

## ✅ 마무리  
tiptab 구현 코드와 spring boot, AWS s3 연동 코드는 Bossi 프로젝트 카테고리에 정리할 예정.

원래 목표는 tiptap 빠르게 마무리하고 redis와 연동해서 장바구니 등등 구현할 예정이었는데 너무 많은 시간을 써서 오늘 목표까지는 구현을 못 했다.

하지만 tiptap 포기 안 하고 사진 넣어서 조금 뿌듯한 것 같기도~  🤪  
