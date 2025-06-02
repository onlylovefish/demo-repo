<template>
  <div class="sao-guang">
    <div class="container">
      <h1 class="txt-swiper">文字扫光</h1>
    </div>

    <!-- 容器扫光 -->
    <!-- 容器扫光不能通过类似文字扫光一样的背景色扫光，因为
      内部可能有元素，会被遮挡，此时可以借助伪元素 -->
    <div
      style="display: flex; flex-direction: column; align-items: center; justify-content: center"
    >
      <div>容器扫光</div>
      <div class="container2">
        <img src="https://avatars.githubusercontent.com/u/65120715?v=4" class="img2" />
      </div>
    </div>
    <!-- 不规则图片扫光 -->
    <div
      style="display: flex; flex-direction: column; align-items: center; justify-content: center"
    >
      <div>不规则图片扫光</div>
      <div class="img-container">
        <img src="../assets/logo.svg" class="img" />
      </div>
    </div>
  </div>
</template>

<style>
.sao-guang {
  display: flex;
}

h1 {
  font-size: 60px;
  font-weight: normal;
  color: hsla(160, 100%, 37%, 1);
}
.txt-swiper {
  width: 300px;
  /* 让文字本身变成透明，配合背景裁剪显示背景色 */
  -webkit-text-fill-color: transparent;
  /* 创建一个45度方向的线性渐变，中间有一条亮色带，两边透明，-100%/50%目的是控制背景初始
  位置和大小 no-repeat currentColor不重复，继承当前文字颜色*/
  background: linear-gradient(
      45deg,
      rgba(255, 255, 255, 0) 40%,
      rgba(255, 255, 255, 0.7),
      rgba(255, 255, 255, 0) 60%
    ) -100%/50%
    no-repeat currentColor;
  /* 让背景只显示在文字形状内 */
  -webkit-background-clip: text;
  /* 扫光动画 */
  animation: shine 3s infinite linear;
}
@keyframes shine {
  /* background-position: 25% 75%
  表示图像上的左侧 25% 和顶部 75% 的位置将放置在距容器左侧 25%
  和距容器顶部 75% 的容器位置 ,详细说明见
  https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position#%E5%85%B3%E4%BA%8E%E7%99%BE%E5%88%86%E6%AF%94%EF%BC%9A*/
  0% {
    background-position: -100% 0;
  }
  100% {
    background-position: 200% 0;
  }
}

.container2 {
  margin-left: 100px;
  display: flex;
  align-items: center;
  overflow: hidden;
}
.img2 {
  width: 200px;
}

.container2::after {
  content: '';
  /* 绝对定位是为了让其在img-container之上 */
  position: absolute;
  background: linear-gradient(
    45deg,
    rgba(255, 255, 255, 0) 40%,
    rgba(255, 255, 255, 0.7),
    rgba(255, 255, 255, 0) 60%
  );
  animation: container-shine 3s infinite linear;
  /* 初始位置在容器左侧外部 */
  transform: translateX(-100%);
  /* 让伪元素比容器大20%，保证动画过程中不回露边 */
  inset: -20%;
}

.img-container {
  background-color: #f0f0f0;
  margin-left: 100px;
  width: 200px;
  height: 200px;
  display: flex;
  align-items: center;
  overflow: hidden;
  /* 不规则的扫光，加一层蒙层 */
  -webkit-mask: url('../assets/logo.svg') no-repeat center;
}

.img-container::after {
  content: '';
  /* 绝对定位是为了让其在img-container之上 */
  position: absolute;
  background: linear-gradient(
    45deg,
    rgba(255, 255, 255, 0) 40%,
    rgba(255, 255, 255, 0.7),
    rgba(255, 255, 255, 0) 60%
  );
  animation: container-shine 3s infinite linear;
  /* 初始位置在容器左侧外部 */
  transform: translateX(-100%);
  /* 让伪元素比容器大20%，保证动画过程中不回露边 */
  inset: -20%;
}
@keyframes container-shine {
  to {
    /* 动画结束时，高光带移动到容器右侧外部 */
    transform: translateX(100%);
  }
}
</style>
