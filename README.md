# Smartprix Laptop Dataset — Data Cleaning

A data cleaning project on laptop listings scraped from [Smartprix](https://www.smartprix.com/), covering 1,020 laptops across 27 features.

---

## Files

| File | Description |
|------|-------------|
| `smartprix_full_df_2.csv` | Raw scraped dataset |
| `data_cleaning.ipynb` | Cleaning notebook |
| `Cleaned.csv` | Final cleaned output |

---

## What the Notebook Does

The raw data had several issues common to scraped e-commerce data:

- **Mixed-up column values** — specs occasionally landed in the wrong column due to inconsistent scraping. A regex-based realignment step detects and corrects these.
- **Dirty string formats** — prices formatted as `₹49,800`, votes as `1,511 votes • 23 reviews`, PPI as `~ 141 PPIAverage`, etc. All converted to clean, usable values.
- **Invalid values** — entries that didn't match a column's expected pattern were replaced with `NaN`.
- **Label noise** — qualitative tags like `"Largest"`, `"Average"`, `"Heavy"` embedded in numeric fields were stripped.
- **Product name** — model name extracted by removing the spec string appended in parentheses.

### Cleaning Steps

1. Thin-space (`\u2009`) removal across all string columns
2. Per-column validation — invalid values replaced with `NaN`
3. Scattered value realignment using regex pattern matching
4. Product name cleanup
5. Type conversions — `price`, `votes`, `ppi` cast to numeric
6. String prefix/label stripping for `os`, `utility`, `thickness`, `weight`, `warranty`, `screen_size`, `resolution`, `battery`, `ram_memory`
7. `screen_feature2` dropped (>55% null); `screen_feature1` renamed to `screen_feature`

---

## Before & After

A few examples of what the cleaning transformed:

| Column | Raw Value | Cleaned Value |
|--------|-----------|---------------|
| `price` | `₹49,800` | `49800` |
| `votes` | `97 votes ` | `97` |
| `ppi` | `~ 141 PPIAverage` | `141` |
| `os` | `OS: Windows 11` | `Windows 11` |
| `utility` | `Utility: Gaming` | `Gaming` |
| `thickness` | `Thickness: 23.5 mmThick` | `23.5mm Thick` |
| `weight` | `2.29 kgHeavy` | `2.29 kg` |
| `warranty` | `1 Year Warranty` | `1 Year` |
| `screen_size` | `15.6 inchesAverage` | `15.6 inches` |
| `resolution` | `1920 x 1080 pixelsAverage` | `1920x1080 px` |

---

## Null Count Summary (Cleaned Dataset)

Remaining nulls reflect genuinely missing specs in the source listings — not cleaning errors.

| Column | Nulls | % Missing |
|--------|-------|-----------|
| `thickness` | 249 | 24.4% |
| `weight` | 110 | 10.8% |
| `screen_feature` | 95 | 9.3% |
| `battery` | 63 | 6.2% |
| `caches` | 38 | 3.7% |
| `processor_speed` | 19 | 1.9% |
| `port_connection` | 15 | 1.5% |
| `warranty` | 9 | 0.9% |
| `usb_ports` | 6 | 0.6% |
| `os` | 5 | 0.5% |
| `no_cores` | 4 | 0.4% |
| `graphics_card` | 3 | 0.3% |
| `hardware_features` | 2 | 0.2% |
| `utility` | 2 | 0.2% |
| `resolution` | 1 | 0.1% |
| `processor_name` | 1 | 0.1% |
| All other columns | 0 | 0% |

---

## Sample Row (Cleaned)

| Field | Value |
|-------|-------|
| `product_name` | HP Victus 15-fb0157AX Gaming Laptop |
| `price` | 49800 |
| `spec_score` | 70 |
| `votes` | 97 |
| `user_rating` | 4.3 |
| `os` | Windows 11 |
| `utility` | Gaming |
| `thickness` | 23.5mm Thick |
| `weight` | 2.29 kg |
| `warranty` | 1 Year |
| `screen_size` | 15.6 inches |
| `resolution` | 1920x1080 px |
| `ppi` | 141 |
| `battery` | 52.5 Wh, 3 Cell Battery |
| `ram_memory` | 8 GB DDR4 RAM |
| `internal_memory` | 512 GB SSD |
| `graphics_card` | 4 GB, AMD Radeon RX 6500M Graphics |
| `wireless_connection` | WiFi, Bluetooth v5.3 |

---

## Dataset Columns

| Column | Description |
|--------|-------------|
| `product_name` | Laptop model name |
| `price` | Price in INR |
| `spec_score` | Smartprix spec score (0–100) |
| `votes` | Number of user votes |
| `user_rating` | Average user rating |
| `os` | Operating system |
| `utility` | Intended use (Gaming, Business, etc.) |
| `thickness` | Physical thickness |
| `weight` | Weight in kg |
| `warranty` | Warranty period |
| `screen_size` | Display size in inches |
| `resolution` | Display resolution |
| `ppi` | Pixels per inch |
| `battery` | Battery capacity |
| `screen_feature` | Display technology / type |
| `processor_name` | CPU name |
| `processor_speed` | CPU clock speed |
| `no_cores` | Number of cores / threads |
| `caches` | Cache size |
| `graphics_card` | GPU |
| `ram_memory` | RAM |
| `internal_memory` | Storage (SSD/HDD) |
| `port_connection` | Port types (HDMI, Thunderbolt, etc.) |
| `wireless_connection` | Wireless standards (WiFi, Bluetooth) |
| `usb_ports` | USB port types |
| `hardware_features` | Extras (Backlit keyboard, Fingerprint sensor, etc.) |

---

## How to Run

1. Clone the repo
2. Install dependencies: `pip install pandas numpy`
3. Place `smartprix_full_df_2.csv` in the same directory
4. Run `data_cleaning.ipynb` top to bottom
