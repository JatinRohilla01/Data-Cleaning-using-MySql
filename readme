
```markdown
# Laptop Price Dataset Cleaning Project

This repository contains the cleaned version of the Uncleaned Laptop Price dataset, which was obtained from an online e-commerce website. The dataset includes information about various laptop models, such as their brand, screen size, processor, memory, storage capacity, operating system, and price.

## Overview

The original dataset was uncleaned, containing missing values, inconsistent formatting, and other errors that needed to be addressed before the data could be used for analysis or modeling. This project aimed to clean the dataset using MySQL queries to make it suitable for analysis.

## Operations Performed on the Data

1. **Create Backup**

    A backup of the original dataset was created to preserve the raw data.

    ```sql
    CREATE TABLE laptop_backup LIKE laptops;
    INSERT INTO laptops_backup SELECT * FROM laptops;
    ```

2. **Check Number of Rows**

    The number of rows in the dataset was checked for reference.

    ```sql
    SELECT COUNT(*) FROM laptops;
    ```

3. **Check Memory Consumption**

    The memory consumption of the dataset was estimated for reference.

    ```sql
    SELECT SUM(TABLE_ROWS * AVG_ROW_LENGTH) / 1024 AS total_data_length_kb
    FROM information_schema.TABLES
    WHERE TABLE_SCHEMA = 'campusx' AND TABLE_NAME = 'laptops';
    ```

4. **Drop Non-Important Columns**

    The "Unnamed" column was dropped from the dataset.

    ```sql
    ALTER TABLE laptops DROP COLUMN `Unnamed: 0`;
    ```

5. **Drop Null Values**

    Rows with null values in essential columns were removed.

    ```sql
    DELETE FROM laptops
    WHERE Company IS NULL
      AND TypeName IS NULL
      AND Inches IS NULL
      AND ScreenResolution IS NULL
      AND Cpu IS NULL
      AND Ram IS NULL
      AND Memory IS NULL
      AND Gpu IS NULL
      AND OpSys IS NULL
      AND Weight IS NULL
      AND Price IS NULL;
    ```

6. **Drop Duplicates**

    No duplicates were found in the dataset.

7. **Change Data Type of Inches Column**

    The data type of the Inches column was changed to Decimal.

    ```sql
    ALTER TABLE laptops MODIFY COLUMN Inches DECIMAL(10,1);
    ```

8. **Clean the Ram Column**

    The Ram column was cleaned to remove "GB" and change the column type to Integer.

    ```sql
    UPDATE laptops SET Ram = REPLACE(Ram, 'GB', '');
    ALTER TABLE laptops MODIFY COLUMN Ram INTEGER;
    ```

9. **Clean Weight Column & Change Column Type**

    The Weight column was cleaned to remove "kg" and changed to Decimal.

    ```sql
    UPDATE laptops SET Weight = REPLACE(Weight,'kg','');
    DELETE FROM laptops WHERE Weight = '?';
    ALTER TABLE laptops MODIFY COLUMN Weight DECIMAL(10,2) DEFAULT 0;
    ```

10. **Round Price Column and Change to Integer**

    The Price column was rounded and changed to Integer.

    ```sql
    UPDATE laptops SET Price = ROUND(Price);
    ALTER TABLE laptops MODIFY COLUMN Price INTEGER;
    ```

11. **Change the OpSys Column**

    Operating system names were standardized.

    ```sql
    UPDATE laptops SET OpSys =
        CASE
            WHEN OpSys LIKE '%mac%' THEN 'macos'
            WHEN OpSys LIKE 'windows%' THEN 'windows'
            WHEN OpSys LIKE '%linux%' THEN 'linux'
            WHEN OpSys = 'No OS' THEN 'N/A'
            ELSE 'other'
        END;
    ```

12. **Change the Gpu Column**

    The Gpu column was split into gpu_brand and gpu_name columns.

    ```sql
    ALTER TABLE laptops ADD COLUMN gpu_brand VARCHAR(255) AFTER Gpu,
    ADD COLUMN gpu_name VARCHAR(255) AFTER gpu_brand;

    UPDATE laptops SET gpu_brand = SUBSTRING_INDEX(Gpu, " ", 1);

    UPDATE laptops SET gpu_name = REPLACE(Gpu, gpu_brand, '');

    ALTER TABLE laptops DROP COLUMN Gpu;
    ```

13. **Change the Cpu Column**

    The Cpu column was split into cpu_brand, cpu_name, and cpu_speed columns.

    ```sql
    ALTER TABLE laptops ADD COLUMN cpu_brand VARCHAR(255) AFTER Cpu,
    ADD COLUMN cpu_name VARCHAR(255) AFTER cpu_brand,
    ADD COLUMN cpu_speed DECIMAL(10,1) AFTER cpu_name;

    UPDATE laptops SET cpu_brand = SUBSTRING_INDEX(Cpu, ' ', 1);

    UPDATE laptops SET cpu_speed = CAST(REPLACE(SUBSTRING_INDEX(Cpu, ' ', -1), 'GHz', '') AS DECIMAL(10,2));

    UPDATE laptops SET Cpu = REPLACE(Cpu, cpu_brand, '');

    UPDATE laptops SET cpu_name = REPLACE(Cpu, SUBSTRING_INDEX(Cpu, ' ', -1), '');

    ALTER TABLE laptops DROP COLUMN Cpu;
    ```

## License

The dataset is sourced from [Kaggle](https://www.kaggle.com/datasets/ehtishamsadiq/uncleaned-laptop-price-dataset) and is subject to the provided [license](https://creativecommons.org/publicdomain/zero/1.0/).

## Author

This cleaning process was performed by Jatin Rohilla. 

Feel free to contribute to this project by forking and submitting pull requests. If you have any questions or suggestions, please feel free to open an issue.

Happy analyzing! 🚀
```
