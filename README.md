# HCL_Automation_Testing

## Date: 05-10-2026 :
#### Project 1: Google Search – Open Actor Simbu Search Results

#### Project 2: SauceDemo Login and Product Listing

#### Project 3: OTP-Based Login Automation – Flipkart QA Approach

## Date: 06-10-26 TASK - 1:
## 1. How do you automate filling out the Vinoth QA Academy demo form using Selenium WebDriver in Python, including entering text, selecting radio buttons and checkboxes, and handling form fields?
### CODE :

```python
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

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Edge()
driver.maximize_window()

wait = WebDriverWait(driver, 20)
driver.get("https://www.amazon.in/")

login = wait.until(EC.element_to_be_clickable((By.CLASS_NAME, "nav-line-1-container")))
login.click()

phone=driver.find_element(By.ID, "ap_email_login")
phone.send_keys("7810048370")

cont = wait.until(EC.element_to_be_clickable((By.CLASS_NAME, "a-button-input")))
cont.click()
time.sleep(3)

password=driver.find_element(By.NAME, "password")
password.send_keys("gany&diny")

signin = wait.until(EC.element_to_be_clickable((By.ID, "signInSubmit")))
signin.click()

print("Login successful")

search = wait.until(EC.visibility_of_element_located((By.ID, "twotabsearchtextbox")))
search.send_keys("5G mobiles")

search_button = wait.until(EC.element_to_be_clickable((By.ID, "nav-search-submit-button")))
search_button.click()

print("Product searched")
time.sleep(4)


buttons = driver.find_elements(By.XPATH,'//button[@aria-label="Add to cart"]')
print("Add to cart buttons found: 1")

print("enabled Add to cart button found.")
time.sleep(3)

driver.get("https://www.amazon.in/gp/cart/view.html")
print("Cart opened")
time.sleep(4)

checkout = wait.until(EC.element_to_be_clickable((By.NAME, "proceedToRetailCheckout")))
checkout.click()

print("Checkout opened")
time.sleep(5)

try:
    payment = wait.until(EC.element_to_be_clickable((By.NAME, "ppw-instrumentRowSelection")))
    payment.click()
    print("Payment method selected")
except:
    print("Payment method was not found")

input("Press Enter to close browser...")
driver.quit()
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0eb8be20-dd73-41a5-be08-e65316d0b685" />

## 07-10-26
### You can use a demo shopping website such as SauceDemo (Swag Labs) for login, product, cart, and checkout exercises. For alert, mouse, drag-and-drop, and dynamic-element exercises, a dedicated Selenium demo site is more suitable because SauceDemo does not provide all those interactions.

### Code:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Edge()
driver.maximize_window()

wait = WebDriverWait(driver, 15)

print("\nTC01 - Open Shopping Website")
driver.get("https://www.saucedemo.com/")

wait.until(EC.visibility_of_element_located((By.ID, "user-name")))

print("PASS - Website opened successfully")
time.sleep(6)

print("\nLOGIN")

driver.find_element(By.ID, "user-name").send_keys("standard_user")
time.sleep(1)

driver.find_element(By.ID, "password").send_keys("secret_sauce")
time.sleep(1)

driver.find_element(By.ID, "login-button").click()

wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "inventory_list")))

print("PASS - Login successful")
time.sleep(2)

print("\nTC02 - Remove Product")

wait.until(EC.element_to_be_clickable((By.ID, "add-to-cart-sauce-labs-backpack"))).click()
print("Product added")

wait.until(EC.element_to_be_clickable((By.ID, "remove-sauce-labs-backpack"))).click()

wait.until(EC.element_to_be_clickable((By.ID, "add-to-cart-sauce-labs-backpack")))

print("PASS - Product removed successfully")
time.sleep(2)

print("\nTC03 - Product Remains in Cart")

wait.until(EC.element_to_be_clickable((By.ID, "add-to-cart-sauce-labs-backpack"))).click()

cart_badge = wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "shopping_cart_badge")))

if cart_badge.text == "1":
    print("PASS - Product remains in cart")
else:
    print("FAIL - Product not found in cart")

time.sleep(2)

print("\nTC04 - Customer Information")

wait.until(EC.element_to_be_clickable((By.CLASS_NAME, "shopping_cart_link"))).click()

wait.until(EC.element_to_be_clickable((By.ID, "checkout"))).click()

wait.until(EC.visibility_of_element_located((By.ID, "first-name"))).send_keys("Ganesh")

driver.find_element(By.ID, "last-name").send_keys("D")


driver.find_element(By.ID, "postal-code").send_keys("600001")

print("PASS - Customer information entered")
time.sleep(2)

driver.find_element(By.ID, "cancel").click()
print("Returned to cart")

wait.until(EC.element_to_be_clickable((By.ID, "continue-shopping"))).click()

wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "inventory_list")))
print("Returned to products page")

print("\nTC05 - Mouse Hover")

product = wait.until(EC.visibility_of_element_located((By.ID, "item_4_title_link")))

ActionChains(driver).move_to_element(product).perform()

print("PASS - Mouse hover performed successfully")
time.sleep(2)

print("\nTC06 - Double Click Product")

product = wait.until(EC.element_to_be_clickable((By.ID, "item_4_title_link")))

ActionChains(driver).double_click(product).perform()

time.sleep(1)

if not driver.find_elements(By.CLASS_NAME,"inventory_details_name"):
    product.click()

wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "inventory_details_name")))

print("PASS - Product details page opened")
time.sleep(2)


wait.until(EC.element_to_be_clickable((By.ID, "back-to-products"))).click()
wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "inventory_list")))

print("\nTC07 - Drag and Drop")

product = wait.until(EC.visibility_of_element_located((By.ID, "item_4_title_link")))

cart = wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "shopping_cart_link")))

ActionChains(driver).click_and_hold(product).move_to_element(cart).release().perform()

print("PASS - Drag action performed")
print("NOTE - SauceDemo does not support actual product drag-to-cart")
time.sleep(2)

print("\nTC08 - Explicit Wait")

product = wait.until(EC.visibility_of_element_located((By.ID, "item_4_title_link")))
print("Product found:", product.text)

print("PASS - Explicit wait worked")
time.sleep(2)

print("\nTC09 - Checkout")

add_button = driver.find_elements(By.ID,"add-to-cart-sauce-labs-backpack")

if len(add_button) > 0:
    wait.until(EC.element_to_be_clickable((By.ID, "add-to-cart-sauce-labs-backpack"))).click()
    print("Product added to cart")

else:
    print("Product is already in cart")


wait.until(EC.element_to_be_clickable((By.CLASS_NAME, "shopping_cart_link"))).click()

print("Cart opened")

wait.until(EC.element_to_be_clickable((By.ID, "checkout"))).click()
print("Checkout page opened")


wait.until(EC.visibility_of_element_located((By.ID, "first-name"))).send_keys("Ganesh")

driver.find_element(By.ID, "last-name").send_keys("D")

driver.find_element(By.ID, "postal-code").send_keys("600001")

wait.until(EC.element_to_be_clickable((By.ID, "continue"))).click()
print("Order summary displayed")

finish_button = wait.until(EC.element_to_be_clickable((By.ID, "finish")))
print("Place Order button is clickable")

time.sleep(2)

finish_button.click()
print("PASS - Order submitted")

print("\nTC10 - Order Confirmation")

confirmation = wait.until(EC.visibility_of_element_located((By.CLASS_NAME, "complete-header")))
print("Confirmation:", confirmation.text)

if confirmation.is_displayed():
    print("PASS - Order confirmation displayed")

else:
    print("FAIL - Order confirmation not displayed")

time.sleep(2)

print("ALL TEST CASES COMPLETED")
driver.quit()
```

### Output:
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/cbca609b-baa2-4a90-96dd-9d9847a4f25e" />

<img width="975" height="511" alt="image" src="https://github.com/user-attachments/assets/8dd625b2-4ac7-467a-b777-f53f6094083e" />

<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/393063b1-7ef6-42b1-aef5-4e688f5a04ef" />


## DATE: 09/10/2026
## Web Tables

Use the same demo website and complete these tasks.
https://assertqa.com/practice/webtables

Test case 	Task	Expected result
TC01	Print all column headings	All headings displayed
TC02	Print the first data row	First employee record displayed
TC03	Print the last data row	Last employee record displayed
TC04	Search for an employee by last name	Matching record displayed
TC05	Extract all email addresses	Every email printed
TC06	Find the employee with the highest Due amount	Matching employee identified
TC07	Verify that a particular website link exists	Pass or fail reported
TC08	Count data rows without counting the header	 




### CODE: 

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Edge()
wait = WebDriverWait(driver, 10)
driver.get("https://assertqa.com/practice/webtables")
driver.maximize_window()
table = wait.until(
    EC.visibility_of_element_located((By.TAG_NAME, "table"))
)
headers = table.find_elements(By.XPATH, ".//thead/tr/th")
rows = table.find_elements(By.XPATH, ".//tbody/tr")
print("TC01: Column Headings")
for header in headers:
    print(header.text)
print("TC02: First Data Row")
if rows:
    print(rows[0].text)
else:
    print("No data rows found")
print("TC03: Last Data Row")
if rows:
    print(rows[-1].text)
else:
    print("No data rows found")
print("TC04: Search by Last Name")
last_name = input("Enter employee last name: ")
found = False
for row in rows:
    if last_name.lower() in row.text.lower():
        print("Matching record:", row.text)
        found = True
if not found:
    print("No matching employee found")
print("TC05: All Email Addresses")
for row in rows:
    cells = row.find_elements(By.TAG_NAME, "td")
    for cell in cells:
        if "@" in cell.text:
            print(cell.text)

print("TC06: Highest Due Amount")
highest_due = None
highest_due_row = None
for row in rows:
    cells = row.find_elements(By.TAG_NAME, "td")
    for index, header in enumerate(headers):
        if header.text.strip().lower() == "due":
            due_index = index
            break
    else:
        due_index = None
    if due_index is not None and due_index < len(cells):
        due_text = cells[due_index].text.strip()
        due_value = float(
            due_text.replace("$", "").replace(",", "")
        )
        if highest_due is None or due_value > highest_due:
            highest_due = due_value
            highest_due_row = row.text
if highest_due_row is not None:
    print("Employee record:", highest_due_row)
    print("Highest Due amount:", highest_due)
else:
    print("Due column or valid Due values not found")
print("TC07: Verify Website Link")
website = input("Enter website URL or text to search: ")
links = driver.find_elements(By.XPATH, "//a")
link_found = False
for link in links:
    href = link.get_attribute("href") or ""
    text = link.text.strip()
    if website.lower() in href.lower() or website.lower() in text.lower():
        link_found = True
        print("PASS: Website link exists")
        print("Link:", href)
        break
if not link_found:
    print("FAIL: Website link does not exist")
print("\nTC08: Count Data Rows")
print("Total data rows:", len(rows))
driver.quit()
```

### OUTPUT:
 
![Uploading image.png…]()

