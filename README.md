# Dyode-Liquid-React-Test

1. Describe how you would make a line of text in a homepage section editable from theme customization and how you would access this in liquid.

    Let's say you have a section file with the following hard-coded line of text in it:
    ```
    <p>Line of hard-coded text.</p>
    ```

    To make this editable, you could edit the section's settings schema and add the following to the settings array:
      ```
      {
        "id": "editable-text",
        "type": "text",
        "label": "Editable Text",
        "default": "Editable Text"
      },
      ```

    Then, to access this in liquid, edit the previously hard-coded line of text from above to read:
    ```
    <p>{{ section.settings.editable-text }}</p>
    ```

2. How would you add the collection featured image as a banner on the collection liquid template?

    At the top of the collection liquid file, add the following:
    ```
    {% if collection.image %}{{ collection.image | img_url: 'master' | img_tag }}{% endif %}
    ```

    To further style the image you could do something like this:
    ```
    {% if collection.image %}<img class="img-to-style" src="{{ collection.image | img_url: 'master' }}" />{% endif %}
    ```

3. Using liquid code and HTML, create a simple pagination container, "< 1 2 ... 5 >".
    ```
    <div class="pagination-container">
      {%- paginate collection.products by 1 -%}
        {%- for product in collection.products -%}
          <!-- show product details here -->
          <h3>{{ product.title }}</h3>
          {{ product | img_url: 'master' | img_tag }}
        {%- endfor -%}

        <div>{{ paginate | default_pagination: next: '>', previous: '<' }}</div>
      {%- endpaginate -%}
    </div>
    ```

4. Using liquid code, access the product named "Blue T-Shirt". Store the id, title, handle, price, url, and image in variables.
    ```
    {%- assign product_id = all_products['blue-t-shirt'].id -%}
    {%- assign product_title = all_products['blue-t-shirt'].title -%}
    {%- assign product_handle = all_products['blue-t-shirt'].handle -%}
    {%- assign product_price = all_products['blue-t-shirt'].price -%}
    {%- assign product_url = all_products['blue-t-shirt'].url -%}
    {%- assign product_image = all_products['blue-t-shirt'].image -%}
    ```

5. Using liquid code, create a key:value array using the list below. Loop through the array. Upon key type, store the value in a variable to be used later:
   - fruit:apple
   - vegetable:carrot
   - cloth:t-shirt
   - denim:jeans

    ```
    {%- assign keyValueArray = "fruit:apple, vegetables:carrot, cloth:t-shirt, denim:jeans" | split: ', ' -%}

    {% for key in keyValueArray %}
      {% assign keyValuePair = key | split: ':' %}
      {% case keyValuePair[0] %}
        {% when "fruit" %}
          {% assign fruitValue = keyValuePair[1] %}
        {% when "vegetables" %}
          {% assign vegetablesValue = keyValuePair[1] %}
        {% when "cloth" %}
          {% assign clothValue = keyValuePair[1] %}
        {% when "denim" %}
          {% assign denimValue = keyValuePair[1] %}
      {% endcase %}
    {% endfor %}
    ```
