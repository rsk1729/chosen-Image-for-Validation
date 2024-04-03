# chosen-Image-for-Validation
Image chosen for width and height fixed and upload mb fixed for this validation
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Questionnaire</title>
    <style>
        .qa-container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
        }

        .question {
            font-weight: bold;
            color: #333;
            margin-bottom: 10px;
        }

        .options {
            margin-left: 20px;
            list-style-type: none;
            padding: 0;
            display: flex;
        }

        .option {
            margin-bottom: 10px;
            width: 200px;
        }

        .option label {
            margin-right: 10px;
        }

        .option input[type="file"] {
            margin-right: 10px;
        }

        .error-message {
            color: red;
            margin-top: 5px;
        }

        button {
            margin-top: 10px;
            padding: 8px 16px;
            background-color: #007bff;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        #previewImage {
            max-width: 100px;
            max-height: 100px;
        }

        /* Styles for the image preview */
        .preview-image {
            width: 50px;
            height: 50px;
            border: 1px solid #ccc;
            margin-bottom: 10px;
            overflow: hidden;
            background: gray;
        }
    </style>
</head>

<body>
    <div class="qa-container">
        <div class="question">Q: Which image represents a cat?</div>
        <ul class="options">
            <li class="option">
                <input type="file" class="image-input" accept=".jpg, .jpeg, .png" onchange="validateImage(this)">
                <p class="error-message" style="color: red; display: none;">Invalid image. Please select a black and
                    white or sketch image.</p>
                <img class="preview-image" src="#">
            </li>
            <li class="option">
                <input type="file" class="image-input" accept=".jpg, .jpeg, .png" onchange="validateImage(this)">
                <p class="error-message" style="color: red; display: none;">Invalid image. Please select a black and
                    white or sketch image.</p>
                <img class="preview-image" src="#">
            </li>
            <li class="option">
                <input type="file" class="image-input" accept=".jpg, .jpeg, .png" onchange="validateImage(this)">
                <p class="error-message" style="color: red; display: none;">Invalid image. Please select a black and
                    white or sketch image.</p>
                <img class="preview-image" src="#">
            </li>
            <li class="option">
                <input type="file" class="image-input" accept=".jpg, .jpeg, .png" onchange="validateImage(this)">
                <p class="error-message" style="color: red; display: none;">Invalid image. Please select a black and
                    white or sketch image.</p>
                <img class="preview-image" src="#">
            </li>
        </ul>
        <button onclick="submitAnswer()">Submit Answer</button>
    </div>

    <script>
        function validateImage(input) {
            var fileInput = input;
            var errorMessage = input.nextElementSibling;
            var previewImage = input.nextElementSibling.nextElementSibling;
            var file = fileInput.files[0];
            if (file) {
                var img = new Image();
                img.src = window.URL.createObjectURL(file);
                img.onload = function () {
                    if (img.width <= 400 && img.height <= 400 && file.size <= 1048576) { // 400x400 pixels and 1MB
                        if (isBlackAndWhite(img) || isDrawingImage(img)) {
                            errorMessage.style.display = 'none';
                            previewImage.src = img.src;
                            previewImage.style.display = 'block';
                        } else {
                            errorMessage.innerText = 'Invalid image. Please upload a black and white or sketch image.';
                            errorMessage.style.display = 'block';
                            fileInput.value = ''; // Clear the file input
                            previewImage.style.display = 'none';
                        }
                    } else {
                        errorMessage.style.display = 'block';
                        fileInput.value = ''; // Clear the file input
                        previewImage.style.display = 'none';
                    }
                };
            }
        }

        function isBlackAndWhite(img) {
            var canvas = document.createElement('canvas');
            var context = canvas.getContext('2d');
            canvas.width = img.width;
            canvas.height = img.height;
            context.drawImage(img, 0, 0);
            var imageData = context.getImageData(0, 0, canvas.width, canvas.height);
            var data = imageData.data;

            // Check if every pixel has similar R, G, and B values
            for (var i = 0; i < data.length; i += 4) {
                if (Math.abs(data[i] - data[i + 1]) > 20 || Math.abs(data[i] - data[i + 2]) > 20 || Math.abs(data[i + 1] - data[i + 2]) > 20) {
                    return false; // Image is not black and white
                } 
            }
            return true; // Image is black and white
        }

        function submitAnswer() {
            var options = document.querySelectorAll('.options .option');
            var selectedImages = [];

            options.forEach(function (option) {
                var previewImage = option.querySelector('.preview-image');
                if (previewImage.src !== "#" && previewImage.style.display === "block") {
                    selectedImages.push(previewImage.src);
                }
            });

            // Now you have an array of selected images
            console.log(selectedImages);
            // You can proceed to process or validate these images as needed
            
        }
    </script>

</body>

</html>
