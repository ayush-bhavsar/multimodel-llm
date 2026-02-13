# Invoice Processing System

An automated invoice data extraction tool powered by **Google Gemini Vision API**. This system processes invoice images in bulk, extracts structured data using AI, categorizes expenses, and exports everything to CSV for easy analysis.

---

## What It Does

1. **Reads** invoice images from a folder
2. **Extracts** key fields (invoice number, date, seller, client, amounts, line items)
3. **Categorizes** each invoice into a business expense category
4. **Exports** all data to a CSV file
5. **Tracks progress** so you can resume if interrupted

---

## Features

| Feature | Description |
|---------|-------------|
| Batch Processing | Process hundreds of invoices in one run |
| AI-Powered Extraction | Uses Gemini 2.5 Flash for accurate OCR and data parsing |
| Auto-Categorization | Assigns expense categories automatically |
| CSV Export | Ready for Excel, Google Sheets, or accounting software |
| Resume Support | Pick up where you left off after interruptions |
| Logging | Detailed logs for debugging and auditing |

---

## Dataset

This project was tested using the **High Quality Invoice Images for OCR** dataset from Kaggle:

**[Download Dataset](https://www.kaggle.com/datasets/osamahosamabdellatif/high-quality-invoice-images-for-ocr)**

The dataset contains high-resolution invoice images suitable for OCR and data extraction tasks.

---

## Expense Categories

The AI assigns one of these categories to each invoice:

| Category | Examples |
|----------|----------|
| Office Supplies | Paper, pens, folders |
| Technology/IT Equipment | Computers, software licenses |
| Professional Services | Consulting, legal fees |
| Marketing/Advertising | Ads, promotional materials |
| Travel & Accommodation | Flights, hotels |
| Utilities | Electricity, internet |
| Maintenance & Repairs | Equipment servicing |
| Food & Beverages | Catering, office snacks |
| Furnitures | Desks, chairs |
| Shoes & Clothing | Uniforms, safety gear |
| Other | Miscellaneous expenses |

---

## Requirements

- **Python 3.8+**
- **Google Gemini API key** (free tier available)

---

## Quick Start

### Step 1: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 2: Set Up API Key

**Option A: Environment Variable**

```powershell
# Windows PowerShell
$env:GEMINI_API_KEY="your_api_key_here"
```

```bash
# Linux/macOS
export GEMINI_API_KEY="your_api_key_here"
```

**Option B: Create a `.env` File**

```
GEMINI_API_KEY=your_api_key_here
```

### Step 3: Add Invoice Images

Place your invoice images in the `invoices/` folder.

**Supported formats:** JPG, JPEG, PNG, GIF, BMP, TIFF

### Step 4: Run the Script

```bash
python process_invoices.py
```

You'll be prompted to choose between test mode (few images) or full processing.

---

## Sample Output

Here are some examples of extracted invoice data from the dataset:

| Invoice | Date | Seller | Client | Category | Items | Total |
|---------|------|--------|--------|----------|-------|-------|
| 11640046 | 11/06/2014 | Atkinson-Woods | Turner Ltd | Technology/IT Equipment | Dell Desktop, Gaming PCs, Ryzen builds | $8,487.82 |
| 69652053 | 11/19/2014 | Sanders, Reed and Olson | Avila Group | Furnitures | Coffee tables, Marble dining table | $15,096.06 |
| 57600191 | 03/17/2017 | McKenzie, Johnson and Rich | Dean Inc | Technology/IT Equipment | Nintendo Switch, Sega CDX, Gameboy, Wii | $2,454.03 |
| 59119338 | 04/11/2017 | Green-Wright | Mosley PLC | Shoes & Clothing | Timberland boots, Soccer cleats, Oxford shoes | $502.74 |
| 97830664 | 09/04/2015 | Bell LLC | Walls Group | Furnitures | Area rugs, Silk carpets, Shaggy rugs | $12,543.64 |
| 69614664 | 11/28/2011 | Compton and Sons | Olson, Simon and Smith | Other | Wine bottle opener | $19.69 |

The AI also provides reasoning for each categorization. For example:
> *"The invoice primarily lists various types of desktop computers and gaming PCs, which clearly fall under the category of Technology/IT Equipment."*

---

## Output

After processing, results appear in the `output/` folder:

```
output/
├── invoice_data.csv    # Extracted data
├── processing.log      # Detailed logs
└── progress.json       # Resume checkpoint
```

### CSV Fields

| Field | Description |
|-------|-------------|
| `invoice_file` | Source image filename |
| `invoice_number` | Invoice ID/number |
| `date` | Invoice date |
| `seller` | Vendor/seller name |
| `client` | Buyer/client name |
| `category` | Assigned expense category |
| `confidence` | AI confidence score |
| `items_found` | Number of line items |
| `reasoning` | Why the category was chosen |
| `total_amount` | Total invoice amount |

---

## Rate Limits

The script handles Gemini API rate limits automatically:
- Adds delays between requests (~4 seconds)
- Retries on rate limit errors
- If you hit daily quota, wait for reset or upgrade your plan

---

## Troubleshooting

| Error | Solution |
|-------|----------|
| "No API key found" | Set `GEMINI_API_KEY` in environment or `.env` file |
| "No image files found" | Add images to `invoices/` folder |
| "Quota exceeded" / HTTP 429 | Wait for quota reset or upgrade plan |
| "JSON parsing error" | Check `processing.log` for details |

---

## Project Structure

```
.
├── invoices/              # Input: Place invoice images here
├── output/                # Output: CSV, logs, progress
├── process_invoices.py    # Main processing script
├── requirements.txt       # Python dependencies
├── QUICKSTART.md          # Quick reference guide
└── README.md              # This file
```

---

## License

Free to use and modify for your needs.

---

**Ready to process invoices? Run `python process_invoices.py` and let the AI do the work!**
