<template>
    <div class="feedback-container">
      <!-- 右下角的觸發按鈕 -->
      <button @click="showModal = true" class="feedback-button">意見反饋</button>
  
      <!-- 意見反饋彈窗 -->
      <div v-if="showModal" class="modal">
        <div class="modal-content">
          <h2>意見反饋</h2>
          <form @submit.prevent="handleSubmit">
            <!-- 類別欄位 -->
            <div class="categoryInput">
              <label for="category">類別</label>
              <select v-model="form.category" id="category">
                <option value="功能建議">功能建議</option>
                <option value="Bug回報">Bug回報</option>
                <option value="其他">其他</option>
              </select>
            </div>
  
            <!-- 標題欄位 -->
            <div class="titleInput">
              <label for="title">標題</label>
              <input v-model="form.title" type="text" id="title" required />
            </div>
  
            <!-- 描述欄位 -->
            <div class="descriptionInput">
              <label for="description">描述</label>
              <textarea v-model="form.description" id="description" required></textarea>
            </div>
  
            <!-- 圖片上傳欄位 -->
            <div class="imageInput">
              <label for="imageUpload">上傳圖片</label>
              <input type="file" @change="handleImageUpload" id="imageUpload" />
              <div v-if="imageDataUrl" class="image-preview">
                <img :src="imageDataUrl" @click="showImagePreview = true" alt="預覽圖" />
                <button @click="removeImage">刪除</button>
              </div>
            </div>
  
            <!-- 提交按鈕 -->
            <button
                class="sumbitBtn"
                type="submit"
            >
                提交
            </button>
          </form>
  
          <!-- 圖片放大預覽彈窗 -->
          <div v-if="showImagePreview" class="image-modal" @click="showImagePreview = false">
            <img :src="imageDataUrl" alt="放大圖" />
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        showModal: false,
        showImagePreview: false,
        form: {
          category: '',
          title: '',
          description: '',
        },
        imageDataUrl: null,
      };
    },
    methods: {
      handleImageUpload(event) {
        const file = event.target.files[0];
        if (file) {
          const reader = new FileReader();
          reader.onload = (e) => {
            this.imageDataUrl = e.target.result;
          };
          reader.readAsDataURL(file);
        }
      },
      removeImage() {
        this.imageDataUrl = null;
      },
      handleSubmit() {
        this.showModal = false;
        alert('提交成功！');
        setTimeout(() => {
          // 模擬5秒後自動關閉彈窗
        }, 5000);
      },
    },
  };
  </script>
  
  <style scoped>
  .feedback-container {
    position: fixed;
    bottom: 20px;
    right: 20px;
  }
  
  .feedback-button {
    padding: 10px 20px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .modal-content {
    background-color: #fff;
    padding: 10px;
    border-radius: 10px;
    width: 1000px;
    height: 500px;
  }

  .image-preview {
    position: relative;
  }
  
  .image-preview img {
    max-width: 100%;
    cursor: pointer;
  }
  
  .image-preview button {
    position: absolute;
    top: 5px;
    right: 5px;
    background-color: red;
    color: white;
    border: none;
    border-radius: 50%;
    cursor: pointer;
  }
  
  .image-modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.8);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .image-modal img {
    max-width: 90%;
    max-height: 90%;
  }
  </style>
  