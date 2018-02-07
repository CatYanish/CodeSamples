```js
//This is the component

import React from 'react'
import PropTypes from 'prop-types'
import { FormattedNumber } from 'react-intl'

const FormattedCurrency = (props) => {
  const { amount } = props

  return (
    <FormattedNumber
      value={amount}
      style="currency"
      currency="USD"
      minimumFractionDigits={amount % 1 !== 0 ? 2 : 0}
      maximumFractionDigits={2}
    />
  )
}

FormattedCurrency.propTypes = {
  amount: PropTypes.number.isRequired,
}

export default FormattedCurrency



//these are the stories
import React from 'react'
import { storiesOf } from '@storybook/react'
import FormattedCurrency from './FormattedCurrency'

storiesOf('atoms/Formats/FormattedCurrency', module)
  .add('With Trailing Zero', () => {
    return (
      <FormattedCurrency amount={3.50}/>
    )
  })
  .add('Without Trailing Zero', () => {
    return (
      <FormattedCurrency amount={3.55}/>
    )
  })
  .add('Whole Number', () => {
    return (
      <FormattedCurrency amount={3}/>
    )
  })
  
  
  //for good measure this is index.js
import FormattedCurrency from './FormattedCurrency'
export default FormattedCurrency



//and for extra extra good measure, this is a file using the new centralized currency format
import React from 'react'
import PropTypes from 'prop-types'
import FormattedCurrency from 'atoms/Formats/FormattedCurrency'

function ContestCollectionData (props) {
  const { lineups } = props

  const collectEntries = (lineups) => lineups.reduce((pValue, cValue) => pValue.concat(cValue.entries), [])
  const entries = collectEntries(lineups)

  const totalWinnings = entries.reduce((pValue, cValue) => pValue + cValue.projectedWinnings, 0)
  const totalEntered = entries.map(entry => entry.contest).reduce((pValue, cValue) => pValue + cValue.entryAmount, 0)

  return (
    <div className="live-contests__contests-data">
      <div className="live-contests__entries o-stat">
        <p className="o-stat__value">{ entries.length }</p>
        <p className="o-stat__label">Total Entries</p>
      </div>
      <div className="live-contests__entries o-stat">
        <p className="o-stat__value">
        //the new component that handles currency formatted is used here
          <FormattedCurrency amount={totalEntered} />
        </p>
        <p className="o-stat__label">Total $ Entered</p>
      </div>
      <div className="live-contests__entries o-stat">
        <p className={`o-stat__value${totalWinnings > 0 ? ' live-contests__is-winning' : ''}`}>
          //the new component that handles currency formatted is used here
          <FormattedCurrency amount={totalWinnings} />
        </p>
        <p className="o-stat__label">Total Winning</p>
      </div>
    </div>
  )
}

ContestCollectionData.propTypes = {
  lineups: PropTypes.array.isRequired,
}

ContestCollectionData.defaultProps = {
  lineups: [],
}

export default ContestCollectionData
```
