---
created: 2025-11-16T20:29
updated: 2025-11-16T20:29
tags:
  - python
---
Radar plot for data per hour for different days

```python
	  categories = pd.Series(df['hour'].unique()).sort_values(ascending=True)
	  categories = [*categories,categories[0]]
	  
	  label_loc = np.linspace(start=0, stop=2*np.pi, num=25,endpoint=True)
	  
	  plt.figure(figsize=(6, 6))
	  ax = plt.subplot(111, polar=True, theta_offset=np.pi/2)
	  
	  for day in pd.Series(df['day'].unique()):
	    data = df.loc[df['day'] == day]
	    data_searches = pd.Series(data['searches_item'])
	    data_searches = [*data_searches, data_searches.iloc[0]]
	    ax.plot(label_loc, data_searches, label=day,c='grey', linewidth=0.8, alpha=0.5)
	  
	  ax.set_xticks(label_loc)
	  ax.set_xticklabels(categories)
	  ax.set_rlabel_position(0)
	  ax.set_theta_direction(-1)
	  plt.title('% of item searches per hour of day', size=20, y=1.05)
	  # plt.legend()
	  plt.show()
