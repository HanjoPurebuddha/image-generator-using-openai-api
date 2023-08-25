const url = "https://api.openai.com/v1/images/generations";
const text = document.getElementById("text");
const image = document.getElementById("image");
const btn = document.getElementById("btn");
const sizeSelect = document.getElementById("sizeSelect");
const numImagesSelect = document.getElementById("numImagesSelect");
const loadingSpinner = document.getElementById("loading");
const apiDiv = document.getElementsByClassName("apiDiv");
const apiInput = document.getElementById("api");

const sizeOptions = ["256", "512", "1024", "1280", "2560", "3840", "5120", "7680"];
const optionsFragment = document.createDocumentFragment();

sizeOptions.forEach((size) => {
  const option = document.createElement("option");
  option.value = size;
  option.textContent = size;
  optionsFragment.appendChild(option);
});

sizeSelect.appendChild(optionsFragment);

for (let i = 1; i <= 10; i++) {
  const option = document.createElement("option");
  option.value = i;
  option.textContent = i;
  numImagesSelect.appendChild(option);
}

let imageSizes = sizeSelect.value;
let numImages = parseInt(numImagesSelect.value);
let apiKey = "";

  function generateImage() {
    if (apiKey === "") {
      apiKey = apiInput.value.trim() || api;
      if (apiKey === "") {
        apiKey = "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"//HY 
        return;
      }
      apiDiv[0].classList.add("hidden");
      apiDiv[1].classList.add("hidden");
    }
    if (text.value === "") {
      alert("Please enter a value");
      return;
    }

    loadingSpinner.classList.remove("hidden");
    btn.disabled = true;

    const data = {
      prompt: text.value,
      n: numImages,
      size: `${imageSizes}x${imageSizes}`,
    };

    fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + apiKey,
      },
      body: JSON.stringify(data),
    })
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        loadingSpinner.classList.add("hidden");
        btn.disabled = false;

        data.data.forEach((item) => {
          const img = document.createElement("img");
          img.src = item.url;
          img.alt = "image";
          img.classList.add(
            "w-full",
            "h-auto",
            "rounded-lg",
            "shadow-lg",
            "hover:shadow-2xl",
            "transition",
            "duration-500",
            "ease-in-out",
            "transform",
            "hover:-translate-y-1",
            "hover:scale-103"
          );

          image.appendChild(img);

          // Double-click event listener
          img.addEventListener("dblclick", () => {
            downloadImage(item.url);
          });
        });
      })
      .catch((err) => {
        console.log(err);
        loadingSpinner.classList.add("hidden");
        btn.disabled = false;
        alert("Something went wrong. Please try again.");
      });
  }

  const checkAuthor = document.getElementById("checkAuthor");
  if (checkAuthor.children[0].children[0].textContent !== "@sauravhathi") {
    window.location.href = "https://github.com/sauravhathi";
  }

  text.addEventListener("input", function () {
    if (text.value === "") {
      btn.classList.remove("bg-slate-900", "text-slate-50");
      text.classList.add("border-r-2", "border-gray-200");
    } else {
      text.classList.remove("border-r-2", "border-gray-200");
      btn.classList.add("bg-slate-900", "text-slate-50");
    }
  });

  sizeSelect.addEventListener("change", function () {
    imageSizes = sizeSelect.value;
  });

  numImagesSelect.addEventListener("change", function () {
    numImages = parseInt(numImagesSelect.value);
  });

  btn.addEventListener("click", generateImage);

  function downloadImage(url) {
    const link = document.createElement("a");
    link.href = url;
    link.download = document.getElementById("text").value.split(" ").join("_") + ".png";
    link.target = "_blank";
    link.click();
  }