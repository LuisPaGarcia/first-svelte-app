<script>
  import Product from "./Product.svelte";
  import Button from "./Button.svelte";
  import Cart from "./Cart.svelte";
  let title = "";
  let price = 0;
  let description = "";

  let products = [];
	let cartItems = [];
  function setTitle(event) {
    title = event.target.value;
  }

  function createProduct() {
    const newProduct = {
      title,
      price,
      description
    };
    products = products.concat(newProduct);
	}
	
	function addToCart(e){
		const selectedTitle = e.detail;
		cartItems = cartItems.concat({...products.find(prod => prod.title === selectedTitle)})
		console.log(cartItems)
	}
</script>
 
<style>
  section {
    max-width: 400px;
    margin: auto;
  }

  label,
  input,
  textarea {
    width: 100%;
  }
</style>

<section>
  <Cart items={cartItems}/>
</section>

<hr />

<section>
  <div>
    <label for="title">Title</label>
    <input type="text" id="title" value={title} on:input={setTitle} />
  </div>
  <div>
    <label for="price">Price</label>
    <input type="number" id="price" bind:value={price} />
  </div>
  <div>
    <label for="price">Description</label>
    <textarea rows="10" bind:value={description} />
  </div>

  <Button on:click={createProduct}>Create Product</Button>
</section>
<section>
  {#if products.length === 0}
    <p>No products yet</p>
  {:else}
    {#each products as product}
      <Product
        productTitle={product.title}
        productPrice={product.price}
        productDescription={product.description} 
				on:addcart={addToCart}
				/>
    {/each}
  {/if}
</section>
