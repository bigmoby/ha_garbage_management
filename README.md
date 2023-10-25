# Home Assistant garbage management schedule
A mini Home Assistant step-by-step tutorial on how to manage your household waste collection calendar using Home Assistant:

### Prerequisites:

* Make sure you have Home Assistant and HACS (Home Assistant Community Store) installed and configured.

+ Install the frontend components `config-template-card` and `button-card` via HACS.

### Creating the Calendar:

* Go to the "Settings" section in your Home Assistant dashboard.

* Under "Device and Services," select "Add Integration."

* Search and select "Local calendar" and add a new calendar, for example, "Glass Collection."

![Add event](new_calendar.png "a title")


* Navigate to the "Calendar" section, and you will find the newly created calendar ("Glass Collection").

![Add event](calendar.png "a title")

* In the calendar section you just created, click on the "Add Event" button to create an event for glass collection. Modify it as follows (for example): 

![Add event](add_event.png "a title")

* Click "Add event" to confirm the addition of the event to the calendar.

### Editing the configuration.yaml for a new Template sensor

* Edit your `configuration.yaml` file and add a new template sensor as follow:

```
template:
  - sensor:
    - name: "glass_collection_schedule"
      state: >-
        {{ min(((state_attr('calendar.glass_collection','start_time') | as_timestamp - today_at('00:00') | as_timestamp) / 86400) | int, 2) }}
      attributes:
        days: >-
          {{ ((state_attr('calendar.glass_collection','start_time') | as_timestamp - today_at('00:00') | as_timestamp) / 86400) | int }}
```

### Lovelace interface configuration

* Download the `bidone_gray.png`, `bidone_orange.png`, and `bidone_green.png` files into the `/config/www/garbage_images` directory. Make sure these files are available in the specified directory. 

* Open a terminal on Home Assistant, then navigate to the `/config/www` directory:

```
cd /config/www
```

* Create a new directory called garbage_images using the following command:
  
```
mkdir garbage_images
```

* Enter the newly created directory:

```
cd garbage_images
```

* Download the files from their respective URLs using the wget command. For example:

```
wget https://example.com/path/to/bidone_gray.png
wget https://example.com/path/to/bidone_orange.png
wget https://example.com/path/to/bidone_green.png
```

Now, you can configure the garbage bin images in the Lovelace interface by using these images from the `/local/garbage_images/` directory.