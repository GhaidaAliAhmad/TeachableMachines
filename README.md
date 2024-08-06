# Teachable Machine 
Teachable Machine is a web-based tool by Google that allows you to create machine learning models without needing to write any code. Here’s a step-by-step guide to get you started:

### Step 1: Access Teachable Machine
1. Open your web browser and go to [Teachable Machine](https://teachablemachine.withgoogle.com/).

### Step 2: Choose a Project Type
2. You'll be prompted to choose the type of project you want to create. The options typically include:
   - Image Project
   - Audio Project
   - Pose Project

### Step 3: Image Project Example
Let's go through an example of creating an image project.

#### Create Classes
3. Click on "Get Started" under the Image Project.
4. You'll see an interface to create classes. A class is a category you want your model to recognize. Click "Add a class" to create multiple classes (e.g., "Class 1" for  golden retriever , "Class 2" for labrador  retriever).

#### Upload Images
5. For each class, you need to provide sample images. You can either:
   - Use your webcam to capture images directly.
   - Upload images from your computer.

6. Make sure to upload a sufficient number of images for each class to improve the model’s accuracy.

### Step 4: Train the Model
7. Once you have your images in place, click on the “Train Model” button. The system will start training your model using the images you provided.

### Step 5: Test the Model
8. After training is complete, you can test your model. Use your webcam or upload an image to see if the model correctly identifies the class.

### Step 6: Export the Model
9. If you're satisfied with the results, you can export the model. Teachable Machine allows you to:
   - Download the model files to use in your own applications.
   - Host the model online and get a link or embed code to use on websites.

### Step 7: Use the Model
10. Depending on how you exported the model, you can integrate it into your projects. If you downloaded the files, you can use them in machine learning frameworks like TensorFlow.js.

### Tips for Better Models
- **Diverse Data**: Use a diverse set of images for each class to make the model robust.
- **Consistent Lighting**: If using a webcam, ensure consistent lighting conditions.
- **Regular Updates**: Continuously update your model with new data to improve accuracy.


## My Link 
https://teachablemachine.withgoogle.com/models/A_ya9jlLQ/

## Photo  
![Screen Shot 1446-02-01 at 11 09 37 PM](https://github.com/user-attachments/assets/2340d73f-03e2-4188-8968-57512dcbdea3)# TeachableMachines


![Screen Shot 1446-02-01 at 11 10 03 PM](https://github.com/user-attachments/assets/67c2210f-da39-4f41-b42a-0877a3ab704f)



![Screen Shot 1446-02-01 at 11 11 01 PM](https://github.com/user-attachments/assets/106f7f7d-4a5c-401e-bc24-33636ab1a385)

#  Java Script 

<div>Teachable Machine Image Model</div>
<button type="button" onclick="init()">Start</button>
<div id="webcam-container"></div>
<div id="label-container"></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js"></script>
<script type="text/javascript">
    // More API functions here:
    // https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image

    // the link to your model provided by Teachable Machine export panel
    const URL = "https://teachablemachine.withgoogle.com/models/A_ya9jlLQ/";

    let model, webcam, labelContainer, maxPredictions;

    // Load the image model and setup the webcam
    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        // load the model and metadata
        // Refer to tmImage.loadFromFiles() in the API to support files from a file picker
        // or files from your local hard drive
        // Note: the pose library adds "tmImage" object to your window (window.tmImage)
        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Convenience function to setup a webcam
        const flip = true; // whether to flip the webcam
        webcam = new tmImage.Webcam(200, 200, flip); // width, height, flip
        await webcam.setup(); // request access to the webcam
        await webcam.play();
        window.requestAnimationFrame(loop);

        // append elements to the DOM
        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) { // and class labels
            labelContainer.appendChild(document.createElement("div"));
        }
    }

    async function loop() {
        webcam.update(); // update the webcam frame
        await predict();
        window.requestAnimationFrame(loop);
    }

    // run the webcam image through the image model
    async function predict() {
        // predict can take in an image, video or canvas html element
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
</script>



