prompt:
A Bio medical equipment list has the following table, I am building an asset management system, where the maintenance departments user(2 or 3), make data entries. They check every information of the asset and analyze whether it needs to be sent for maintenance and many other things like checking a certain asset and whatever requires in asset management. Many departments can view and download  an excel sheet about all the information about the asset. I will be using Django for this:

Table column headers:
 Location, Room No, User, Equipment name, Assets No, Model No, Serial no, Quantity, Manufacturers, Origin, Vendor, Installation date, Values

# Location is which department is using eg. Neuro, GOPD, Cornea. data type = (character)
# Room No. eg. 405,40(0),40(1). data type (int)
# User eg. Doctor, Optometrist. data type= str
# Equipment Name eg. Slit Lamp,  Retinoscope. data type = char
# Assets No eg. N/A , ieh-2124-SL-13
# Model No eg. CT-700, AR-1
# Serial No eg. N/A, 124553
# Manufacturer eg. Nidek, Dell
# Origin eg. Japan, Germany, UK
# Vendor eg. Fashion Optics, Iris Enterprise
# Installation dates eg. 10/11/2025
# Value eg. 12454.00, 45000.00 ( all currency amount )
