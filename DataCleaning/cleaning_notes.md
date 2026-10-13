The dataset is largely cleaned and consistent, but will benefit from some general preprocessing. We are primarily concerned with data redundancy, inconsistencies in date formatting, empty attribute values, and multi-value data.

By observation and by declaration of the dataset author, 
- the Cast and Crew tables contain denormalized movie_title and movie_release_date attributes, alongside some other movie metadata spread around the tables. These can be eliminated or their data can be moved into a movie entity or a new related table, which will reduce redundancy in our final database.
- By observation, there are inconsistencies in date formatting, where different attributes that contain date information across different tables may contain date and time information, or just date information, etc. Largely, the format YYYY-MM-DD is utilized, but we will need to verify that no anomalies or errors have snuck in anywhere, which we can do by plotting a general timeline and checking for unexpected values (like dates far in future or far in the past) before inserting them into our database. 
- Lastly, the genre attribute of the movie entity is currently formatted as a comma-delimited list, which will need to be restructured. This should be stored as a multi-value attribute, so we will need to split up the contents of the genre attribute values before they are inserted into our database. 

We expect to use Python to clean up the dataset and write the results back to the CSV to be inserted into a database later into the project.
After loading the dataset, we would like to 
- first eliminate redundant data (for example, the movie_title attribute on Cast entities) because that will let us deal with less data while executing the remaining processing.
- Then, we plan to deal with date format inconsistency, first by splitting up datetime values into separate attributes for date and for time, and then by checking, per table, that there are no timeline outliers.
- In the event that few extreme outliers exist, it may be possible to manually correct the date, but that will be dependent on how many arise, in which case we may have to deal with each table with a specialized script to reformat dates. Similarly, depending on the quantity of empty values, we might be able to find and add values to our dataset if necessary. 
- However, the poster of the dataset describes that some attributes for some rows are left empty if data was not made public or is otherwise unknown, in which case we think it is appropriate to use a more explicit indicator that the value was intentionally left empty. 
- Finally, our script will also be able to split up the contents of the Movie entity’s genres attribute, but this may be better executed immediately before insertion into our final database.


### My observation

- What should I do with NaN values?
- 