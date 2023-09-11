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
  
지금까지 진행한 프로젝트는 글 안에 이미지를 넣는게 아니라 먼저 넣은 이미지가 다 보이고 그 밑으로 내용이 보이도록 구현했다.  
이번 프로젝트에서는 내용 안에 원하는 이미지를 넣어서 볼 수 있도록 구현을 하고 싶었다.  
  
인터넷으로 찾아보니 Tiptap이라는 라이브러리를 이용하면 원하는대로 구현이 가능했다.  

[https://tiptap.dev/](https://tiptap.dev/)
  
![tiptap-editor.png](/assets/images/TIL/project/0911/tiptap-editor.png)  
  
tiptab 홈페이지 문서를 따라서 작성하니 글을 작성하는건 구현이 완료 되었으나 사진을 중간 중간에 넣을 수 있는 방법을 몰랐다.  
  
[https://tiptap.dev/api/nodes/image](https://tiptap.dev/api/nodes/image)  
이 페이지를 따라서 실행을 하면 이미지 url을 넣으면 사진이 글 상자 안으로 넣을 수 있었다.  
하지만 내가 원하는건 이미지를 내 컴퓨터에서 가지고 오는 방법이었다.  

  
구글에 여러가지 키워드로 검색하고 챗 GPT에 물어도 봤지만 제대로 구현이 되지않았다.    

[How to upload images with Tiptap editor](https://gist.github.com/slava-vishnyakov/16076dff1a77ddaca93c4bccd4ec4521)    
[Adding drag and drop image uploads to Tiptap](https://www.codemzy.com/blog/tiptap-drag-drop-image)  
  
  
    

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
  
  
Spring boot와 aws s3를 연동시키고, 이미지를 업로드 누르면 aws s3에 저장이 되도록 구현을 했다.  
  
그럼 여기서 문제점은 판매자가 선택한 사진은 이미 클라우드에 올라가 있는 상태고 작성을 하다가 사진이 필요가 없어서 지우게 된다면, 필요없는 데이터만 쌓이게 되는것이다.  
이 해결 방법은 선택한 이미지의 이름을 배열로 갖고 있다가 판매자가 글을 작성하고 저장을 누를때 이미지의 이름들을 백으로 넘겨서 있는지 확인하고 없을 경우 지우도록 구현을 할 예정이다.  
  
![uploadImg1.png](/assets/images/TIL/project/0911/uploadImg1.png)  

![uploadImg2.png](/assets/images/TIL/project/0911/uploadImg2.png)   
  

![uploadImg3.png](/assets/images/TIL/project/0911/uploadImg3.png)
  

## ✅ 마무리
원래 목표는 tiptap 빠르게 마무리하고 redis와 연동해서 장바구니등등 구현할 예정이었는데 너무 많은 시간을 써서 오늘 목표까지는 구현을 못했다.  
하지만 tiptap 포기안하고 사진 넣어서 조금 뿌듯한것 같기도~  🤪