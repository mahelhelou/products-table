# Documentation

[Project Link](https://reactjs.org/docs/thinking-in-react.html)

## Step 1: Start With A Mock

The first thing you’ll want to do is to draw boxes around every component (and subcomponent) in the mock and give them all names. If you’re working with a designer, they may have already done this, so go talk to them! Their Photoshop layer names may end up being the names of your React components!

### UI Components

- **FilterableProductTable (orange):** contains the entirety of the example
- **SearchBar (blue):** receives all user input
- **ProductTable (green):** displays and filters the data collection based on user input
- **ProductCategoryRow (turquoise):** displays a heading for each category
- **ProductRow (red):** displays a row for each product

### UI Compoents Hierarchy

- FilterableProductTable
  - SearchBar
  - ProductTable
    - ProductCategoryRow
    - ProductRow

## Step 2: Build A Static Version in React

### HTML

```html
<div id="root"></div>
```

### CSS

```css
body {
	padding: 5px;
}
```

### JS

```js
function ProductCategoryRow(props) {
	return (
		<tr>
			<th colSpan='2'>{props.category}</th>
		</tr>
	)
}

function ProductRow(props) {
  return (
    <tr>
      <td>{props.name}</td>
      <td>{product.price}</td>
    </tr>
  )
}

class ProductRow extends React.Component {
	render() {
		const product = this.props.product
		const name = product.stocked ? product.name : <span style={{ color: 'red' }}>{product.name}</span>

		return (

		)
	}
}

class ProductTable extends React.Component {
	render() {
		const rows = []
		let lastCategory = null

		this.props.products.forEach(product => {
			if (product.category !== lastCategory) {
				rows.push(<ProductCategoryRow category={product.category} key={product.category} />)
			}
			rows.push(<ProductRow product={product} key={product.name} />)
			lastCategory = product.category
		})

		return (
			<table>
				<thead>
					<tr>
						<th>Name</th>
						<th>Price</th>
					</tr>
				</thead>
				<tbody>{rows}</tbody>
			</table>
		)
	}
}

class SearchBar extends React.Component {
	render() {
		return (
			<form>
				<input type='text' placeholder='Search...' />
				<p>
					<input type='checkbox' /> Only show products in stock
				</p>
			</form>
		)
	}
}

class FilterableProductTable extends React.Component {
	render() {
		return (
			<div>
				<SearchBar />
				<ProductTable products={this.props.products} />
			</div>
		)
	}
}

const PRODUCTS = [
	{ category: 'Sporting Goods', price: '$49.99', stocked: true, name: 'Football' },
	{ category: 'Sporting Goods', price: '$9.99', stocked: true, name: 'Baseball' },
	{ category: 'Sporting Goods', price: '$29.99', stocked: false, name: 'Basketball' },
	{ category: 'Electronics', price: '$99.99', stocked: true, name: 'iPod Touch' },
	{ category: 'Electronics', price: '$399.99', stocked: false, name: 'iPhone 5' },
	{ category: 'Electronics', price: '$199.99', stocked: true, name: 'Nexus 7' }
]

ReactDOM.render(<FilterableProductTable products={PRODUCTS} />, document.getElementById('container'))
```
