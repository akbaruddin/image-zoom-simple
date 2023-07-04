<script>
  // Exported props
  export let imageStyle = {};
  export let containerStyle = {};
  export let url = null;
  export let zoomImgUrl = null;
  export let viewerWidth = 200;
  export let viewerHeight = 400;
  export let selectorWidth = 30;
  export let selectorHeight = 30;

  // Internal state and variables
  let zoomStyle = { left: 0, top: 0 };
  let viewerImageStyle = { left: 0, top: 0 };
  let realProps = { width: 0, height: 0 };
  let SPACING = 15;
  const imageUrl = zoomImgUrl ? zoomImgUrl : url;
  let refImage;
  let show = false;

  // Helper function to compute inline styles
  const computeStyle = (style) =>
    Object.entries(style)
      .map((ms) => `${ms[0]}:${ms[1]}`)
      .join(",");

  const onLoad = (e) => {
    realProps = { width: e.target.width, height: e.target.height };
  };

  const onMove = (e) => {
    const halfSWidth = selectorWidth / 2;
    const halfSHeight = selectorHeight / 2;
    let realX;
    let realY;

    const localX = e.clientX - e.target.offsetLeft;
    const localY = e.clientY - e.target.offsetTop;

    if (localX < halfSWidth) {
      realX = 0;
    } else if (localX + halfSWidth > e.target.offsetWidth) {
      realX = e.target.offsetWidth - selectorWidth;
    } else {
      realX = localX - halfSWidth;
    }

    if (localY < halfSHeight) {
      realY = 0;
    } else if (localY + halfSHeight > e.target.offsetHeight) {
      realY = e.target.offsetHeight - selectorHeight;
    } else {
      realY = localY - halfSHeight;
    }

    zoomStyle = { left: realX, top: realY };

    const viewerX =
      realX *
      ((realProps.width - viewerWidth) /
        (refImage.offsetWidth - selectorWidth));
    const viewerY =
      realY *
      ((realProps.height - viewerHeight) /
        (refImage.offsetHeight - selectorHeight));

    viewerImageStyle = { left: -viewerX, top: -viewerY };
  };

  const onEnter = () => {
    show = true;
  };

  const onOut = () => {
    show = false;
  };
</script>

<div
  class="zoom-box"
  style={computeStyle(containerStyle)}
  on:mousemove={onMove}
  on:mouseenter={onEnter}
  on:mouseleave={onOut}
>
  <img src={url} bind:this={refImage} alt="" style={computeStyle(imageStyle)} />
  <div
    class="viewer-box"
    class:show
    style="left: {SPACING +
      refImage?.offsetWidth}px;width: {viewerWidth}px; height: {viewerHeight}px;"
  >
    <img
      src={imageUrl}
      on:load={onLoad}
      alt=""
      style="top: {viewerImageStyle.top}px;left: {viewerImageStyle.left}px;"
    />
  </div>
  <div
    class="zoom-selector"
    class:show
    style="left: {zoomStyle.left}px; top: {zoomStyle.top}px;width: {selectorWidth}px; height:{selectorHeight}px"
  />
</div>

<style>
  .zoom-box {
    display: inline-block;
    position: relative;
  }

  .zoom-box > img {
    pointer-events: none;
    display: block;
  }

  .viewer-box {
    position: absolute;
    border: 1px solid rgb(239, 237, 240);
    overflow: hidden;
    z-index: 999;
    top: 0;
    display: none;
  }

  .viewer-box img {
    position: absolute;
  }

  .zoom-selector {
    position: absolute;
    background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAIAAAACCAMAAABFaP0WAAAABGdBTUEAAK/INwWK6QAAABl0RVh0U29mdHdhcmUAQWRvYmUgSW1hZ2VSZWFkeXHJZTwAAAAGUExURT1uzv///62t27cAAAACdFJOU/8A5bcwSgAAABBJREFUeNpiYGBkYGQECDAAAA0ABMZIs2EAAAAASUVORK5CYII=");
    background-repeat: repeat;
    pointer-events: none;
    cursor: crosshair;
    display: none;
    z-index: 9;
  }

  .zoom-selector.show,
  .viewer-box.show {
    display: block;
  }
</style>
