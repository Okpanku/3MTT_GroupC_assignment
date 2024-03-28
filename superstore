import streamlit as st
import pandas as pd
import os
import plotly.express as px
from sklearn.cluster import KMeans


st.title("3MTT GROUP C DATA ANALYSIS AND VISUALIZATION ASSIGNMENT")
st.title("Analysis of Sales at a Superstore in the US")
st.sidebar.title("Random Orders Analysis Dashboard")

# Load the dataset
BASE_DIR = os.path.dirname(os.path.abspath(__file__))
DATA_URL = os.path.join(BASE_DIR, "superstore.csv")

def load_data():
    # Specify the encoding as 'latin1' or 'ISO-8859-1'
    data = pd.read_csv(DATA_URL, encoding='latin1')
    data['Order Date'] = pd.to_datetime(data['Order Date'], format='%d/%m/%Y')
    return data

data = load_data()

st.markdown("### The Superstore Dataset")
st.write(data)

# Sidebar options
st.sidebar.subheader('Show random orders')
random_order = st.sidebar.radio("Ship Mode", data['Ship Mode'].unique())
random_data = data[data['Ship Mode'] == random_order].sample(n=1)
st.sidebar.markdown("### Random Order Details")
st.sidebar.write(random_data)

st.sidebar.subheader("Orders Count by Ship Mode")
select = st.sidebar.selectbox('Visualization type', ['Histogram', 'Piechart'], key='select_widget')
ship_mode_count = data['Ship Mode'].value_counts().reset_index()
ship_mode_count.columns = ['Ship Mode', 'Orders Count']

st.title("Orders Count by Ship Mode")
if not st.sidebar.checkbox("Hide", True):
    st.markdown('### Number of Orders by Ship Mode')
    if select == 'Histogram':
        fig = px.bar(ship_mode_count, x='Ship Mode', y='Orders Count', height=500)
        st.plotly_chart(fig)
    else:
        fig = px.pie(ship_mode_count, values='Orders Count', names='Ship Mode')
        st.plotly_chart(fig)
        
        
st.title("Average Delivery Time of Processed Orders")        
# Calculate average delivery time
average_delivery_time = data['Processing_Time'].mean()
st.write(f"Average Delivery Time: {average_delivery_time} days")

# Distribution of delivery times using a histogram with Plotly Express
fig = px.histogram(data, x='Processing_Time', nbins=30, title='Distribution of Delivery Times')
fig.update_layout(xaxis_title='Delivery Time (days)', yaxis_title='Frequency')
st.plotly_chart(fig)



import streamlit as st
import pandas as pd
import plotly.express as px

# Assuming 'data' is your DataFrame containing the order data with the 'State' and 'Sales' columns
def load_data():
    # Load your dataset
    # data = pd.read_csv("your_dataset.csv")
    return data

data = load_data()



st.title("Geographic Analysis of Sales by State")
# Coordinates of each state in the USA
state_coordinates = {
    'Alabama': (32.806671, -86.791130),
    'Alaska': (61.370716, -152.404419),
    'Arizona': (33.729759, -111.431221),
    'Arkansas': (34.969704, -92.373123),
    'California': (36.116203, -119.681564),
    'Colorado': (39.059811, -105.311104),
    'Connecticut': (41.597782, -72.755371),
    'Delaware': (39.318523, -75.507141),
    'Florida': (27.766279, -81.686783),
    'Georgia': (33.040619, -83.643074),
    'Hawaii': (21.094318, -157.498337),
    'Idaho': (44.240459, -114.478828),
    'Illinois': (40.349457, -88.986137),
    'Indiana': (39.849426, -86.258278),
    'Iowa': (42.011539, -93.210526),
    'Kansas': (38.526600, -96.726486),
    'Kentucky': (37.668140, -84.670067),
    'Louisiana': (31.169546, -91.867805),
    'Maine': (44.693947, -69.381927),
    'Maryland': (39.063946, -76.802101),
    'Massachusetts': (42.230171, -71.530106),
    'Michigan': (43.326618, -84.536095),
    'Minnesota': (45.694454, -93.900192),
    'Mississippi': (32.741646, -89.678696),
    'Missouri': (38.456085, -92.288368),
    'Montana': (46.921925, -110.454353),
    'Nebraska': (41.125370, -98.268082),
    'Nevada': (38.313515, -117.055374),
    'New Hampshire': (43.452492, -71.563896),
    'New Jersey': (40.298904, -74.521011),
    'New Mexico': (34.840515, -106.248482),
    'New York': (42.165726, -74.948051),
    'North Carolina': (35.630066, -79.806419),
    'North Dakota': (47.528912, -99.784012),
    'Ohio': (40.388783, -82.764915),
    'Oklahoma': (35.565342, -96.928917),
    'Oregon': (44.572021, -122.070938),
    'Pennsylvania': (40.590752, -77.209755),
    'Rhode Island': (41.680893, -71.511780),
    'South Carolina': (33.856892, -80.945007),
    'South Dakota': (44.299782, -99.438828),
    'Tennessee': (35.747845, -86.692345),
    'Texas': (31.054487, -97.563461),
    'Utah': (40.150032, -111.862434),
    'Vermont': (44.045876, -72.710686),
    'Virginia': (37.769337, -78.169968),
    'Washington': (47.400902, -121.490494),
    'West Virginia': (38.491226, -80.954681),
    'Wisconsin': (44.268543, -89.616508),
    'Wyoming': (42.755966, -107.302490)
}

# Add 'Lon' and 'Lat' columns based on state_coordinates
data['Lon'] = data['State'].map(lambda state: state_coordinates[state][1])
data['Lat'] = data['State'].map(lambda state: state_coordinates[state][0])

# Create a scatter map to visualize sales by state
fig_map = px.scatter_geo(data, lat='Lat', lon='Lon', color='Sales', size='Sales',
                         hover_name='State', title='Sales Distribution by State',
                         projection='albers usa', labels={'Sales': 'Total Sales ($)'},
                         color_continuous_scale='Blues')

# Customize map layout
fig_map.update_geos(visible=False, showcountries=False, showcoastlines=False,
                    showland=False, showlakes=False, showrivers=False,
                    showsubunits=True, subunitcolor="rgb(0, 0, 0)")

# Show the map
st.plotly_chart(fig_map)



st.title("Product Quantity Breakdown by Sub-Category")
# Calculate quantity of products purchased by sub-category
sub_category_quantity = data.groupby('Sub-Category')['Quantity'].sum().reset_index()

# Create a bar chart to visualize the quantity of products purchased for each sub-category
fig_bar = px.bar(sub_category_quantity, x='Sub-Category', y='Quantity', title='Quantity of Products Purchased by Sub-Category')
fig_bar.update_layout(xaxis_title='Sub-Category', yaxis_title='Quantity')
st.plotly_chart(fig_bar)

