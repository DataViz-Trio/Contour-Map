# Contour-Map

## Dataset Description:

- The color mapping and contour plot datasets follow the following pattern:
- The First Six lines of the dataset provide some information about the dataset such as the variable being plotted (surface rain rate in our case), the Flag which denotes a bad value (-999 in this dataset), the number of rows and columns in the dataset and the date on which the data was collected.
- From the 7th line, the data is presented. The dataset follows the following pattern:
- Each column corresponds to a longitude. The longitudes begin at 0.125E.
- Each row corresponds to a latitude. The latitudes begin at 89.875S and ends at 89.875N.
- Each cell corresponding to a column (longitude) and a row (latitude) contains the sea surface rain rate at that longitude and latitude.
- Our group had chosen April - May 2016 as the months for performing the Color Mappings. Hence, we chose 10 dates: 
    - 1, 10, 20, 30 April 2016
    - 10, 20, 30 April 2016
    - 10, 20, 30 June 2016 

## Color Mapping Data Processing: 

- We ignore the first 7 lines and start reading the text file from the 8th line. We ignore the 7th line as well since the longitudes in the dataset are in the same order that the library expects. Hence, we do not need to explicitly store the longitudes to perform any sort of data processing later on.
- We store each line in a list. We drop the first element of each list, which corresponds to the latitude for that line. The reason for dropping the latitude is the same as the reason for dropping the longitudes. 
- Due to the limitation of ASCII Text files, certain rows contain the message ** line too long ** at the end of the line.
- We split the line at all the spaces. If the last element of the line contains ** line too long **, we pop the last element out of the list. We then convert all strings (the surface rain rates) to their float values. 
- Due to the limitation of Text files, not all rows contain 1440 values. Hence, we keep adding the BAD VALUE to the list until the length of the list is 1440. 
- All these lists (rows) are added to another list to generate a 2D list.

## Color Mapping Implementation

- The *generate_dataset(name)* is a function that takes in a name of the text file (dataset), processes it and returns a 2D List, as described in the Data Processing section.

- The *plot_contour(data,title,contour_levels,contour_colors)* generates a contour plot using the Matplotlib and Cartopy libraries. The implementation of the method is as follows:

    - Input Parameters:
        - data: A 2D array-like data representing values for the contour plot.
        - title: A string containing the title of the contour plot.
        - contour_levels: A list of contour levels to be displayed on the plot. These levels represent the constant values of the contour lines.
        - contour_colors: A list defining colors for the contour lines corresponding to different contour levels.

    - Plot Initialization:
        - Initializes a contour plot using Matplotlib and Cartopy with Plate Carrée projection centered at longitude 180.
        - Applies a dark background style to enhance visualization.

    - Plot Data: The data is plotted on the map using the *contour* function which takes the data parameter to extract values for contour lines. Additionally, it uses contour_levels to determine where to draw the lines and contour_colors to assign colors to the lines.

    - Map Features: The function adds coastlines to the map using *add_feature()* to provide geographic context.

    - Colorbar: The *fig.colorbar()* function takes contour_plot (the contour lines) as input, ticks specifies the values at which tick marks will be placed on the color bar, orientation determines the direction of the color bar ('vertical' in this case), label provides a label for the color bar.

    - Display the Plot: The function displays the plot using plt.show().