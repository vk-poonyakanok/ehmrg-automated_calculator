# EHMRG Automation Tool

This repository contains a Python-based automation tool for calculating the **Emergency Heart Failure Mortality Risk Grade (EHMRG)** score using the MDCalc website. The tool uses Selenium WebDriver to interact with the web interface and process batch calculations for provided input data.

## Features

- Automatically inputs data from an Excel file into the EHMRG calculator.
- Extracts the results (EHMRG Score, Mortality Percentage, Risk Category) from the website.
- Handles edge cases like low oxygen saturation (adjusted to a minimum value of 41 if lower).
- Detects and resolves duplicate EHMRG scores due to fast processing by re-running specific rows.
- Saves the output to a new Excel file for easy analysis.

## Prerequisites

- **Python 3.8+**
- **Google Chrome** and the appropriate [ChromeDriver](https://chromedriver.chromium.org/downloads)
- Packages:
  - `selenium`
  - `pandas`
  - `pyperclip`
  - `openpyxl`

## Usage

### Steps to Use the Repository

1. **Prepare the Data**
   - Create an Excel file with the following columns:
     - `Age`: Patient's age in years.
     - `SBP`: Systolic blood pressure in mmHg.
     - `HR`: Heart rate in beats per minute.
     - `Spo2RA`: Oxygen saturation percentage.
     - `Cr`: Creatinine level in mg/dL.
     - `K`: Potassium level.
     - `Transport by EMS`: 1 for Yes, 0 for No.
     - `Troponin Positive`: 1 for Yes, 0 for No.
     - `Active cancer`: 1 for Yes, 0 for No.
     - `On metolazone`: 1 for Yes, 0 for No.

   - Save the file as `EHMRG_data.xlsx`.

2. **Run the Script**
   - Log in manually to the MDCalc website when prompted.
   - The script will:
     - Process each row from the input Excel file.
     - Extract results (EHMRG Score, Mortality Percentage, Risk Category).
     - Detect duplicate EHMRG scores in consecutive rows and reprocess them.

4. **Output**
   - The results will be saved to an Excel file named `EHMRG_results.xlsx`.

---

## Data Description

| **Column Name**        | **Description**                                                          |
|-------------------------|--------------------------------------------------------------------------|
| `Age`                  | Patient's age in years.                                                 |
| `SBP`                  | Systolic blood pressure in mmHg.                                        |
| `HR`                   | Heart rate in beats per minute.                                         |
| `Spo2RA`               | Oxygen saturation in percentage. Values below 40 are adjusted to 40.    |
| `Cr`                   | Creatinine level in mg/dL.                                              |
| `K`                    | Potassium level.                                                        |
| `Transport by EMS`     | Indicates if the patient was transported by EMS (1 = Yes, 0 = No).      |
| `Troponin Positive`    | Indicates if the troponin test was positive (1 = Yes, 0 = No).          |
| `Active cancer`        | Indicates if the patient has active cancer (1 = Yes, 0 = No).           |
| `On metolazone`        | Indicates if the patient is on metolazone (1 = Yes, 0 = No).            |
| `EHMRG`                | Calculated EHMRG score extracted from MDCalc.                           |
| `Percent`              | Mortality risk percentage extracted from MDCalc.                        |
| `Text`                 | Risk interpretation extracted from MDCalc.                              |

---

## Limitations

- Designed for **non-dialysis patients** as per the EHMRG guidelines.
- The tool relies on the **stability and consistency** of the MDCalc website layout.
- Results are dependent on the **accuracy of user-provided data**.

---

## Disclaimer

This tool is intended for **research and educational purposes only**. All calculations must be rechecked by a clinician before use. The author of this repository is not responsible for any medical decisions based on the output of this tool.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## References

1. **[EHMRG Calculator on MDCalc](https://www.mdcalc.com/calc/1755/emergency-heart-failure-mortality-risk-grade-ehmrg)**
2. Lee, D. S., et al. “Prediction of heart failure mortality in emergent care: a cohort study.” *PubMed*. [Link](https://pubmed.ncbi.nlm.nih.gov/22665814/)
3. “Prospective Validation of the Emergency Heart Failure Mortality Risk Grade for Acute Heart Failure.” *PubMed*. [Link](https://pubmed.ncbi.nlm.nih.gov/30586748/)
