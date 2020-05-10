# CardPointe Gateway Tokenizer for React.js

**Authored By: [NativeStack Engineering](https://www.upwork.com/ag/nativestack/)**

## Product Under Development and Not Live

We are working with CardConnect to provide a fully customizeable and PCI compliant solution for modern web frameworks. We did not expect this package to be as popular as it turned out to be. We are still testing the features in this package and working to make it compatible across as many different platforms as possible. Please contact us at **(628) 400 2701** or email us at **Support@NativeStack.io** for help implementing this service into your project until we have ths package ready.

CardConnect's CardPointe Hosted iFrame Tokenizer & PCI Compliant CardSecure tokenization package to securely authorize & capture transactions with NativeStack & CardPointe for React.js applications.

## Installation

`npm install react-cardpointe-gateway`

### Implementation

This module requires [`react-bootstrap` v^1.0.0-beta.12 as a _peer dependancy_](https://react-bootstrap.netlify.app). You can install the version needed after reviewing the doc with:

`npm install react-bootstrap@1.0.0-beta.12`

In the example `<App />` included in the package we first implement the following imports:

    import Form from 'react-bootstrap/Form'
    import Container from 'react-bootstrap/Container'
    import { NativeStackTokenizer } from 'react-cardpointe-gateway'

In the `constructor` of the parent component with the implementation of the component, declare a state attribute as such:

```
    constructor(props) {
    	super(props);
        this.state = {
        	emvData: ""
        };
    }
```

Next implement a `componentDidUpdate()` function as such:

```
	componentDidUpdate() {
		console.log('This is the TokenData: ', this.state.emvData)
		/* NOTE: This is the function passed into props
		 *
		 *       This will send token data back to Parent component
		 *
		 *       @return {token: "9418594164541111", expiryDate: "202312"}
		 */
		/*
			Use this function if you will embed this component as a child into
			a parent component so you can recursively send the emvData in state
			back up into the parent component where this component will reside.
				try {
					this.props.tokenProps.userEmvData(this.state.emvData)
				} catch (err) {
					console.log('UPDATING CARD')
				}
		*/
	}
```

Next, implement this function in your parent component to be used by the `react-cardpointe-gateway` tokenizer. This needs to go in the same file where you will call your component from.

```
    /* NOTE:
     * @function userEmvData
     * @param emvData
     * Parent component must implement function
     * to pass emvData returned from child into
     * state.
     */
    userEmvData = (emvData) => {
    	this.setState({
    		emvData: emvData,
    	});
    };
```

The `render` function in your parent component needs to declare an object that will be used to pass the authentication data needed by the payment gateway to tokenize any credit card securely and in compliance with PCI with an implementation like the example below:

```
    render() {
    	/* NOTE:
    	* @const tokenProps
    	* Parent component must declare tokenProps
    	* in render function to pass userEmvData
    	* function into child component props.
    	*/
    	const tokenProps = {
    		// below is token info
    		userEmvData: this.userEmvData,
    	};
    	/*
    	* NOTE: User has to pass tokenProps into props
    	*       for child component to allow this to access
    	*       the function in parent component.
    	*/
    	return (
    		<Container className='payments'>
    			{/* Start Form for step 1 here!! */}
    			{/* onSubmit={ this.handleSubmit } */}
    			<Form className='form-renewals' method='post'>
    				{/* This is the Number FG */}
    				<Form.Group
    					controlId='tokenEvent'
    					className='billing-group'
    				>
    					<NativeStackTokenizer
    						site='fts'
    						port='6443'
    						tokenProps={tokenProps}
    					/>
    				</Form.Group>
    			</Form>
    		</Container>
    	);
    }
```

### License

**IPA**

**Contact: Support@NativeStack.io**

#### Keywords

payments, merchant-account, emv-token, react, card-pointe, native-stack, card-secure, card-connect, credit-cards, pci-compliant
