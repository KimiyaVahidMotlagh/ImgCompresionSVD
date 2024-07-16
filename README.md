# ImageCompresion
A project for compresing images using SVD algorithm. The script splits the image into its red, green, and blue color channels, applies SVD to each channel, and then reconstructs 
the image with reduced dimensions. This compression technique can significantly reduce the size of the image while preserving its visual quality.

## Tabel of content
- [Requirements](https://github.com/KimiyaVahidMotlagh/ImgCompresionSVD/tree/main#requirements) <br/>
- [Code Explanation](https://github.com/KimiyaVahidMotlagh/Threeway_Mergesort/blob/main/README.md#advantages) <br/>
- [Usage](https://github.com/KimiyaVahidMotlagh/Three-way-Merge-sort/blob/main/README.md#run-and-evaluation) <br/>

## Requirements
This project uses [Numpy](https://numpy.org/) and [PIL](https://pillow.readthedocs.io/en/stable/reference/Image.html)
libraries.

## Code Explanation
The compress_color_image function performs the following steps: <br/>
#### 1. Load Images:
```Python
image = Image.open(image_path)
A = np.array(image)
```
#### 2. Split color channels
```Python
R = A[:,:,0]
G = A[:,:,1]
B = A[:,:,2]
```
#### 3. Compress each channel using SVG
```Python
def compress_channel(channel):
    U, sigma, VT = np.linalg.svd(channel, full_matrices=False)
    U_k = U[:, :k]
    sigma_k = np.diag(sigma[:k])
    VT_k = VT[:k, :]
    return np.dot(U_k, np.dot(sigma_k, VT_k))

R_k = compress_channel(R)
G_k = compress_channel(G)
B_k = compress_channel(B)
```
#### 4. Reconstruct and Save the image
```Python
compressed_image_array = np.stack([R_k, G_k, B_k], axis=2)
compressed_image_array = np.clip(compressed_image_array, 0, 255)
compressed_image = Image.fromarray(compressed_image_array.astype('uint8'))
compressed_image.save(output_path)
```
## Usage
1. Save the code file and move it to the image folder <br/>
2. Rename the last code line <br/> 
3. Run the code
