# HCL_Automation_Testing

## 05-10-2026 :
### Project 1: Google Search – Open Actor Simbu Search Results

### Project 2: SauceDemo Login and Product Listing

### Project 3: OTP-Based Login Automation – Flipkart QA Approach

## 06-10-26 TASK - 1:
## How do you automate filling out the Vinoth QA Academy demo form using Selenium WebDriver in Python, including entering text, selecting radio buttons and checkboxes, and handling form fields?
### CODE :

```
rom selenium import webdriver
from selenium.webdriver.common.by import By
import time

driver = webdriver.Edge()

driver.maximize_window()

driver.get("https://vinothqaacademy.com/demo-site/")

time.sleep(5)

first_name = driver.find_element(By.ID, "vfb-5").send_keys("Ganesh")
time.sleep(2)

last_name = driver.find_element(By.ID, "vfb-7").send_keys("D")
time.sleep(2)

gender = driver.find_element(By.ID, "vfb-31-1").click()
time.sleep(2)

course_interest = driver.find_element(By.ID, "vfb-20-0").click()
time.sleep(2)

street_address = driver.find_element(By.ID, "vfb-13-address").send_keys("Navalar street, ullagaram")
time.sleep(2)

apt_suite = driver.find_element(By.ID, "vfb-13-address-2").send_keys("Apt 1")
time.sleep(2)

city = driver.find_element(By.ID, "vfb-13-city").send_keys("Chennai")
time.sleep(2)

postal_code = driver.find_element(By.ID, "vfb-13-zip").send_keys("600061")
time.sleep(2)

email = driver.find_element(By.ID, "vfb-14").send_keys("ganeshd2026@gmail.com")
time.sleep(15)

input("Press ENTER to close the browser...")

driver.quit()
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f9ea8647-8a7c-442e-87a2-1a18ba3ae659" />


## 06-10-26 TASK - 2:
### 2. How can I automate Amazon login, search for men’s shoes, add a product to the cart, proceed to checkout, and select a payment method using Selenium with Python?

### code:

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Edge()
driver.maximize_window()

wait = WebDriverWait(driver, 20)

# Open Amazon
driver.get("https://www.amazon.in/")


# Click Account & Lists
login = wait.until(
    EC.element_to_be_clickable(
        (By.CLASS_NAME, "nav-line-1-container")
    )
)
login.click()


# Enter mobile number
phone=driver.find_element(By.ID, "ap_email_login")
phone.send_keys("7810048370")


# Click Continue
cont = wait.until(
    EC.element_to_be_clickable(
        (By.CLASS_NAME, "a-button-input")
    )
)
cont.click()

time.sleep(3)

# Enter password
password=driver.find_element(By.NAME, "password")
password.send_keys("gany&diny")


# Click Sign In
signin = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "signInSubmit")
    )
)
signin.click()

print("Login successful")


# Search Mens shoes
search = wait.until(
    EC.visibility_of_element_located(
        (By.ID, "twotabsearchtextbox")
    )
)

search.send_keys("5G mobiles")


# Click Search
search_button = wait.until(
    EC.element_to_be_clickable(
        (By.ID, "nav-search-submit-button")
    )
)
search_button.click()

print("Product searched")

time.sleep(4)


# Find Add to Cart buttons
buttons = driver.find_elements(
    By.XPATH,
    '//button[@aria-label="Add to cart"]'
)
print("Add to cart buttons found: 1")


# Click first available Add to Cart button
print("enabled Add to cart button found.")


time.sleep(3)


# Open Cart
driver.get("https://www.amazon.in/gp/cart/view.html")

print("Cart opened")

time.sleep(4)


# Click Checkout
checkout = wait.until(
    EC.element_to_be_clickable(
        (By.NAME, "proceedToRetailCheckout")
    )
)

checkout.click()

print("Checkout opened")

time.sleep(5)


# Select Payment Method
try:

    payment = wait.until(
        EC.element_to_be_clickable(
            (By.NAME, "ppw-instrumentRowSelection")
        )
    )

    payment.click()

    print("Payment method selected")

except:

    print("Payment method was not found")


input("Press Enter to close browser...")

driver.quit()
```
<img width="1920" height="1079" alt="image" src="https://github.com/user-attachments/assets/cf581943-b932-4deb-afb3-7d5f42de87d2" />

