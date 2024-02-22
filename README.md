# Support-Spot
Resource locater
from geopy.geocoders import Nominatim
import folium

def get_location_coordinates(address):
    geolocator = Nominatim(user_agent="resource_locator")
    location = geolocator.geocode(address)
    return (location.latitude, location.longitude)

def create_map(location, zoom_level=12):
    map_object = folium.Map(location=location, zoom_start=zoom_level)
    return map_object

def add_marker(map_object, location, popup_text):
    folium.Marker(location, popup=popup_text).add_to(map_object)

if __name__ == "__main__":
    # Example usage
    address = "123 Main Street, City, Country"  # Replace with the address you want to locate
    coordinates = get_location_coordinates(address)

    resource_map = create_map(coordinates)

    # Example markers, you can customize this based on the services you want to locate
    marker1_location = (coordinates[0] + 0.001, coordinates[1] + 0.001)
    marker1_popup_text = "Shelter A"
    add_marker(resource_map, marker1_location, marker1_popup_text)

    marker2_location = (coordinates[0] - 0.001, coordinates[1] - 0.001)
    marker2_popup_text = "Rehabilitation Center B"
    add_marker(resource_map, marker2_location, marker2_popup_text)

    # Save the map as an HTML file or display it in your application
    resource_map.save("resource_locator_map.html")
