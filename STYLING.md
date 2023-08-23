List of colors to style plots. Try to make this human and machine readable. For example, if the format is 'NAME: `HEX_COLOR`' it will render nicely in the markdown file and will be readable using regular expressions. For example, in python you could use this code:
```python
import re

# Initialize our dictionary
color_dict = {}

# Open the file and read each line
with open('STYLING.md','r') as f:
  # Read in the next line
  cur_line_text = f.readline()
  # Apply our regex expression for matching our format
  match = re.search('([^:]+):\s*`#([A-F0-9]+)`', cur_line_text)
  if match:
    color_dict[match.group(1)] = {'HEX': match.group(2), ...
      'RGB': [int(match.group(2)[0:2], 16), int(match.group(2)[2:4], 16), int(match.group(2)[4:], 16)]}

# Now you can use this in your plots
plt.plot(data_x, data_y, color=color_dict['PFC, line'].HEX)

```
PFC, line: `#DD1523`

PFC, area: `#DD1523`

IT, line: `#222288`

IT, area: `#222288`
