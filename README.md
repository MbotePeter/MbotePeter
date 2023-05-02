$(function() {
  // Add event listeners to the product buttons
  $(".product button").on("click", function() {
    // Get the product ID
    const productId = $(this).data("product-id");

    // Add the product to the cart
    addToCart(productId);
  });

  // Add event listener to the checkout button
  $("#checkout-button").on("click", function() {
    // Get the cart total
    const cartTotal = calculateCartTotal();

    // Show a confirmation dialog
    $("#confirmation-dialog").textContent = `Are you sure you want to checkout for ${cartTotal}?`;
    $("#confirmation-dialog").style.display = "block";

    // Add a handler to the "Confirm" button
    $("#confirm-button").on("click", () => {
      // Hide the confirmation dialog
      $("#confirmation-dialog").style.display = "none";

      // Do something with the cart, such as sending it to the server
    });
  });
});

// Add a product to the cart
function addToCart(productId) {
  // Get the cart element
  const cart = $("#cart");

  // Create a new item element
  const item = document.createElement("li");

  // Set the item's text
  item.textContent = productId;

  // Add the item to the cart
  cart.appendChild(item);
}

// Calculate the total price of the cart
function calculateCartTotal() {
  // Get the cart element
  const cart = $("#cart");

  // Initialize the total price to 0
  let totalPrice = 0;

  // Iterate over the items in the cart
  for (const item of cart.children) {
    // Get the product ID from the item
    const productId = item.textContent;

    // Get the product price
    const productPrice = parseFloat(productId);

    // Add the product price to the total price
    totalPrice += productPrice;
  }

  // Return the total price
  return totalPrice;
}

