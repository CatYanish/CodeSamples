
```js

import React from 'react'
import { styled } from 'utils/style'

const ErrorMessage = styled.div`
    color: red;
`

const SuccessName = styled.div`
    color: green;
`

const MyFirstComponent = (props) => {
    if(!props.firstName) {
        return <MySecondComponent message="Please enter a first name"/>
    } 
    if(!props.lastName) {
        return <MySecondComponent message="Please enter a last name"/>
    } 
    return (
        <SuccessName>Yay {props.firstName} {props.lastName}</SuccessName>
    )
}

function MySecondComponent(props) {
    return (
        <ErrorMessage>{props.message}</ErrorMessage>
    )
}

export default MyFirstComponent
```
