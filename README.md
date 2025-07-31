Muhammad Ribfli_4222201014

# OCR License Plate Recognition with Vision Language Models

A Python application that performs Optical Character Recognition (OCR) on Indonesian license plates using Vision Language Models (VLMs) through LMStudio API. The system evaluates OCR accuracy using Character Error Rate (CER) metrics.

## Features

- **Multi-model Support**: Compatible with various VLMs through LMStudio
- **Automatic API Detection**: Tests multiple LMStudio configurations automatically
- **Performance Evaluation**: Calculates Character Error Rate (CER) for accuracy assessment
- **Batch Processing**: Processes entire datasets efficiently
- **CSV Output**: Exports results with ground truth comparisons
- **Error Handling**: Robust error handling with detailed logging

## Requirements

### Software Dependencies
```bash
pip install requests
pip install rapidfuzz
```

### System Requirements
- **LMStudio**: Must be running locally with API enabled
- **Python 3.7+**
- **Vision Language Model**: Compatible VLM loaded in LMStudio (default: gemma-3-4b-it-qat)

## Installation

1. **Clone or download the notebook**
2. **Install required packages**:
   ```bash
   pip install requests rapidfuzz
   ```
3. **Set up LMStudio**:
   - Download and install [LMStudio](https://lmstudio.ai/)
   - Load a vision-capable model (e.g., gemma-3-4b-it-qat)
   - Start the local server with API enabled

## Configuration

Update the configuration variables in the notebook:

```python
DATASET_PATH = "/path/to/your/dataset/images"  # Path to test images
LABEL_CSV = "label.csv"                        # Ground truth labels file
OUTPUT_CSV = "license_plate_ocr_results.csv"  # Output results file
SELECTED_MODEL_NAME = "gemma-3-4b-it-qat"     # Model name in LMStudio
```

## Dataset Structure

### Image Dataset
```
dataset/
├── images/
│   ├── test/
│   │   ├── plate001.jpg
│   │   ├── plate002.png
│   │   └── ...
```

### Ground Truth CSV Format
The `label.csv` file should contain:
```csv
image_filename,license_plate_text
plate001.jpg,B1234ABC
plate002.png,D5678XYZ
```

## Usage

### Running the Application

1. **Start LMStudio** with your chosen vision model
2. **Prepare your dataset** and ground truth CSV file
3. **Run the notebook** cells in order:
   ```python
   # The main() function will:
   # 1. Test LMStudio API connectivity
   # 2. Load ground truth data
   # 3. Process all images in the dataset
   # 4. Calculate CER scores
   # 5. Generate results CSV
   ```

### API Configuration Testing
The application automatically tests these LMStudio configurations:
- `http://localhost:1234/v1/chat/completions`
- `http://127.0.0.1:1234/v1/chat/completions`
- `http://localhost:8080/v1/chat/completions`

## Output

### Results CSV
The output file contains:
- **image**: Processed image filename
- **ground_truth**: Expected license plate text
- **prediction**: Model's OCR prediction
- **CER_score**: Character Error Rate (0.0 = perfect, 1.0 = completely wrong)

### Console Output
```
Testing LMStudio configurations...
Found working API at: http://localhost:1234
Using model: gemma-3-4b-it-qat
Loading ground truth from: label.csv
Starting OCR processing...

Processing plate001.jpg...
GT: B1234ABC | Pred: B1234ABC | CER: 0.0000

Average CER Score: 0.1250
```

## Performance Metrics

### Character Error Rate (CER)
CER is calculated using the Levenshtein distance:
```
CER = Levenshtein_distance(prediction, ground_truth) / len(ground_truth)
```

- **0.0**: Perfect match
- **0.1**: 10% character error rate
- **1.0**: Completely incorrect

## Troubleshooting

### Common Issues

1. **LMStudio API not reachable**
   - Ensure LMStudio is running
   - Check that API server is enabled in LMStudio settings
   - Verify the model is loaded and ready

2. **Ground truth file not found**
   - Check the `LABEL_CSV` path
   - Ensure CSV format is correct (filename, label)

3. **Image processing errors**
   - Verify image file formats (jpg, jpeg, png)
   - Check file permissions
   - Ensure images exist in the specified path

4. **Model timeout errors**
   - Increase timeout value in the request
   - Check model performance and system resources

### Error Codes in Output
- **FORMAT_ERROR**: Unexpected API response format
- **ERROR**: General processing error (network, file access, etc.)

## Model Compatibility

Tested with:
- **Gemma 3 4B IT**: Good performance on Indonesian license plates

## Contributing

To improve the system:
1. Add support for additional image formats
2. Implement more sophisticated text preprocessing
3. Add support for different license plate formats
4. Include confidence scores in output

