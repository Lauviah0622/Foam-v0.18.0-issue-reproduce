

## get start


## story


```js
import React from 'react';

import { Button } from './Button';

export default {
  title: 'Button',
  component: Button,
};
// story 的基本資料

export const Primary = () => <Button primary>Button</Button>; // 這個就是個別的 story　　
export const Primary = () => <Button primary label="Button"/>;
Primary.storyName = 'I am the primary'; // 夏名字

export const WithHook = () => {

  // Sets the hooks for both the label and primary props
  const [value, setValue] = useState('Secondary');
  const [isPrimary, setIsPrimary] = useState(false);

  // Sets a click handler to change the label's value
  const handleOnChange = () => {
    if (!isPrimary) {
      setIsPrimary(true);
      setValue('Primary');
    }
  };
  return <Button primary={isPrimary} onClick={handleOnChange} label={value} />;
};


export const Secondary = () => <Button backgroundColor="#ff0" label="😄👍😍💯" />;

export const Secondary = Template.bind({});
Secondary.args = { ...Primary.args, label: '😄👍😍💯' };
// 比較


```