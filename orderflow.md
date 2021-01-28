## Order Flow Testing Scenarios

### Develop an understanding of the platform
http://docs.opencart.com/en-gb/store-front/

### Test Scenarios
**Disclaimer:** Each requirement being tested can be found in the software documentation. Unfortunately there are no page subsections available to make navigating the documentation easier, so I'll be referring to a section heading in the document relevant to each scenario.

Additionally the documentation does not provide a clear outline of what each feature is capable of doing, or how it should function. Assumptions will be made for the purpose of this assignment.

#### Log into account
**Heading:** "Creating an account"

**Testing Technique:** Decision Table. Refer to account module. 

When signing in to your account, you need to provide your account email and the case sensitive password that's associated with it.

#### Use the search field to find a product
**Heading:** "Navigating the shop"

**Testing Technique:** Functional Testing

Products are defined by various different attributes such as name, brand and description. Finding a product by comparing the content entered into the search field against product attributes should return results where a majority of the search value can be found within the products attributes. 

#### Use Category Product Listings to find products
**Heading:** Category product listings

**Testing Technique:** User interface and Usability testing

A category is a means of grouping similar products into a single location to provide the end user a fast and seamless method of finding what they're looking for. Identifying that each category is accurately defined and not providing irrelevant products will improve user experience.

#### Add product to cart
**Heading:** Featured products, Category product listings, Product pages and Product comparison

**Testing Technique:** Dynamic testing or Decision table

Products have different attributes that can change the way that the product is interacted with when attempting to add it to cart. Attributes such as Stock, Product options and minimum order quantity. These attributes in combination decides whether a product will be added to the cart, have the browser perform a page redirect or highlight input fields that do not pass validation.

#### View product page
**Heading:** Browsing the storefront

**Testing Technique:** Assertion testing

When redirected to a product page, validation needs to be performed that the product which was selected is actually the product that is being displayed, as well as making sure that the product attributes are pulled correctly and not failing, or pulling incorrect information.

#### Start the checkout process
**Heading:** Shopping cart page

**Testing Technique:** Vulnerability Testing

As a whole the checkout process consists of various different parts that should be tested in isolation as they all interact with the cart in different ways, but the most important factor would be to ensure that there are steps in place to mitigate risk of users potentially purchasing a product without needing to pay for it out of their own pocket.

[Return to README](https://github.com/seth-rah/OC-HA/blob/main/README.md)