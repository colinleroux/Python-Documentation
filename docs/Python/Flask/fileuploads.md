# File uploads

### 1. **Setting Up Your Flask Application**

First, you need to set up your Flask application and configure it to handle file uploads. Here’s a simple configuration:

```python
from flask import Flask

app = Flask(__name__)
app.config['UPLOAD_FOLDER'] = 'uploads/'  # Folder to store uploaded files
app.config['MAX_CONTENT_LENGTH'] = 16 * 1024 * 1024  # Limit upload size to 16MB
```

### 2. **Creating an Upload Form**

You can create an HTML form for file uploads. Using Tailwind CSS for styling, it might look like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Upload Image</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.0.0/dist/tailwind.min.css" rel="stylesheet">
</head>
<body>
    <div class="container mx-auto p-4">
        <h1 class="text-2xl">Upload an Image</h1>
        <form action="/upload" method="post" enctype="multipart/form-data">
            <input type="file" name="file" accept="image/*" class="border rounded p-2">
            <button type="submit" class="bg-blue-500 text-white rounded p-2 mt-2">Upload</button>
        </form>
    </div>
</body>
</html>
```

### 3. **Handling File Uploads in Flask**

You’ll need a route to handle the file upload. Here’s an example:

```python
from flask import request, redirect, url_for, render_template
import os

@app.route('/upload', methods=['POST'])
def upload_file():
    if 'file' not in request.files:
        return 'No file part'
    file = request.files['file']
    
    if file.filename == '':
        return 'No selected file'

    if file:
        filename = secure_filename(file.filename)
        file.save(os.path.join(app.config['UPLOAD_FOLDER'], filename))
        return redirect(url_for('upload_success'))

@app.route('/upload/success')
def upload_success():
    return 'File uploaded successfully!'
```

### 4. **Image Previews**

For image previews before upload, you can use JavaScript. Here's an example using plain JavaScript:

```html
<input type="file" id="fileInput" accept="image/*" onchange="previewImage()">
<img id="preview" src="#" alt="Image Preview" style="display:none;">

<script>
function previewImage() {
    const file = document.getElementById('fileInput').files[0];
    const reader = new FileReader();
    
    reader.onloadend = function() {
        const preview = document.getElementById('preview');
        preview.src = reader.result;
        preview.style.display = 'block';
    }
    
    if (file) {
        reader.readAsDataURL(file);
    }
}
</script>
```

### 5. **Resizing and Reorienting Images**

For image processing, you can use the **Pillow** library. To install it, run:

```bash
pip install Pillow
```

Here’s how you can resize and reorient images after upload:

```python
from PIL import Image

def resize_image(file_path, output_size=(300, 300)):
    with Image.open(file_path) as img:
        img.thumbnail(output_size)
        img.save(file_path)

@app.route('/upload', methods=['POST'])
def upload_file():
    # (previous code)
    
    if file:
        filename = secure_filename(file.filename)
        file_path = os.path.join(app.config['UPLOAD_FOLDER'], filename)
        file.save(file_path)
        
        # Resize image
        resize_image(file_path)
        
        return redirect(url_for('upload_success'))
```

### 6. **Handling Orientation Issues**

You can check the EXIF data of the image to handle orientation:

```python
from PIL import ExifTags

def correct_image_orientation(file_path):
    with Image.open(file_path) as img:
        for orientation in ExifTags.TAGS.keys():
            if ExifTags.TAGS[orientation] == 'Orientation':
                break
        exif = img._getexif()
        if exif is not None:
            orientation_value = exif.get(orientation)
            if orientation_value is not None:
                # Rotate image based on orientation_value
                if orientation_value == 3:
                    img = img.rotate(180, expand=True)
                elif orientation_value == 6:
                    img = img.rotate(270, expand=True)
                elif orientation_value == 8:
                    img = img.rotate(90, expand=True)
        img.save(file_path)
```

### 7. **Integrating Everything**

Integrate the resizing and orientation correction in your upload handler:

```python
@app.route('/upload', methods=['POST'])
def upload_file():
    # (previous code)

    if file:
        filename = secure_filename(file.filename)
        file_path = os.path.join(app.config['UPLOAD_FOLDER'], filename)
        file.save(file_path)

        # Resize and correct orientation
        correct_image_orientation(file_path)
        resize_image(file_path)
        
        return redirect(url_for('upload_success'))
```

## Multiple file uploads

To implement multiple file uploads with previews in Flask, you can follow a
similar approach as before but modify the HTML form and JavaScript to 
accommodate multiple files. Here's a step-by-step guide:

### 1. **Update the HTML Form**

You need to allow multiple file uploads in the HTML form. 
You can achieve this by adding the `multiple` attribute to the file input. 
Here’s how the updated form looks:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Upload Images</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.0.0/dist/tailwind.min.css" rel="stylesheet">
    <style>
        .preview {
            display: inline-block;
            margin: 10px;
        }
        .preview img {
            max-width: 150px;
            max-height: 150px;
        }
    </style>
</head>
<body>
    <div class="container mx-auto p-4">
        <h1 class="text-2xl">Upload Images</h1>
        <form action="/upload" method="post" enctype="multipart/form-data">
            <input type="file" id="fileInput" name="files" accept="image/*" multiple class="border rounded p-2">
            <div id="previewContainer"></div>
            <button type="submit" class="bg-blue-500 text-white rounded p-2 mt-2">Upload</button>
        </form>
    </div>

    <script>
        function previewImages() {
            const files = document.getElementById('fileInput').files;
            const previewContainer = document.getElementById('previewContainer');
            previewContainer.innerHTML = ''; // Clear previous previews
            
            for (let i = 0; i < files.length; i++) {
                const reader = new FileReader();
                reader.onloadend = function() {
                    const div = document.createElement('div');
                    div.className = 'preview';
                    const img = document.createElement('img');
                    img.src = reader.result;
                    img.alt = 'Image Preview';
                    div.appendChild(img);
                    previewContainer.appendChild(div);
                }
                reader.readAsDataURL(files[i]);
            }
        }

        document.getElementById('fileInput').addEventListener('change', previewImages);
    </script>
</body>
</html>
```

### 2. **Handle Multiple File Uploads in Flask**

Next, update your Flask route to handle multiple files. You can access the uploaded files from `request.files` and iterate through them. Here’s the modified route:

```python
from flask import request, redirect, url_for, render_template
import os
from werkzeug.utils import secure_filename

@app.route('/upload', methods=['POST'])
def upload_files():
    if 'files' not in request.files:
        return 'No file part'
    
    files = request.files.getlist('files')  # Get list of uploaded files
    
    if not files:
        return 'No selected files'

    uploaded_files = []
    
    for file in files:
        if file:
            filename = secure_filename(file.filename)
            file_path = os.path.join(app.config['UPLOAD_FOLDER'], filename)
            file.save(file_path)
            uploaded_files.append(filename)  # Store uploaded filenames for later use
            
            # You can also resize and correct orientation for each file
            correct_image_orientation(file_path)
            resize_image(file_path)

    return redirect(url_for('upload_success'))

@app.route('/upload/success')
def upload_success():
    return 'Files uploaded successfully!'
```

### 3. **Image Resizing and Orientation Correction**

You can reuse the image resizing and orientation correction functions defined earlier. They will be called for each uploaded image inside the loop in the `upload_files` route.

### Summary

With these updates, you can now upload multiple images and display previews for each one. The backend can handle the uploaded files as a list, allowing you to perform any necessary processing (like resizing and correcting orientation) for each image individually. This approach ensures a smooth user experience, similar to what you might have implemented in Laravel and Livewire.
