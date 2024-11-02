# showing-the-code-snippet-for-LIST-BY-AVAILABILITY-test-case
def test_list_products_by_availability(self):
    # Create products with different availability statuses
    available_product = Product(name="ToyRobot", category="Electronics", available=True)
    unavailable_product = Product(name="OldToy", category="Vintage", available=False)
    available_product.save()
    unavailable_product.save()
    
    # Send a request to list available products
    response = self.client.get("/products?available=true")
    
    # Assert only available products are listed
    assert response.status_code == 200
    assert all(product['available'] is True for product in response.json)
