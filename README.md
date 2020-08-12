# TMSupport4

Приложение используется для непрерывной работы технической поддержки . Обеспечивает учет заявок и рабочего времени.

## Установка и запуск


All the steps below should be executed in a cmder console window.
Clone the Vespa sample apps from github:
```bash
- git clone https://github.com/vespa-engine/sample-apps.git
- set VESPA_SAMPLE_APPS="%CD%\sample-apps"
```
**Start a Vespa Docker container:**
```bash
- docker run --detach --name vespa --hostname vespa-container --privileged --volume %VESPA_SAMPLE_APPS%:/vespa-sample-apps --publish 8080:8080 vespaengine/vespa
```
**Wait for configuration server to start - wait for a 200 OK response:**
```bash
- docker exec vespa bash -c "curl -s --head http://localhost:19071/ApplicationStatus"
```
**Deploy and activate a sample application:**
```bash
- docker exec vespa bash -c "/opt/vespa/bin/vespa-deploy prepare /vespa-sample-apps/basic-search/src/main/application"
- docker exec vespa bash -c "/opt/vespa/bin/vespa-deploy activate"
```
**Ensure the application is active - wait for a 200 OK response:**
```bash
- curl -s --head "http://localhost:8080/ApplicationStatus"
```
**Feed documents:**
```bash
- cat %VESPA_SAMPLE_APPS%/basic-search/music-data-1.json | curl -s -H "Content-Type:application/json" --data-binary @- "http://localhost:8080/document/v1/music/music/docid/1"
- cat %VESPA_SAMPLE_APPS%/basic-search/music-data-2.json | curl -s -H "Content-Type:application/json" --data-binary @- "http://localhost:8080/document/v1/music/music/docid/2"
```
**Run a query post or get request :**
```bash
- curl -s -H "Content-Type: application/json" --data '{"query" : "bad"}' http://localhost:8080/search/ | python -m json.tool
- curl -s http://localhost:8080/search/?query=bad | python -m json.tool
View the results in a browser in the GUI for building queries at http://localhost:8080/querybuilder/, which can help you building queries with e.g. autocompletion of YQL, or at http://localhost:8080/search/?query=bad. Read more in the Search API.
```
**Run a document get request:**
```bash
- curl -s http://localhost:8080/document/v1/music/music/docid/2 | python -m json.tool
```
**Stop the running container when you no longer need it:**
```bash
    - docker stop vespa
```
**Optionally, remove the stopped container entirely:**
```bash
    - docker rm vespa
```
### Prerequisites

	1 [docker](https://docs.docker.com/engine/installation/) installed.
	2 [cmder](http://cmder.net/) full version installed.
	3 Operating system: Microsoft Windows 10  Pro (Docker requirement).
	4 Architecture: x86_64 .
	5 *At least 4GB* of memory dedicated to your container instance.


### Installing

    -The application created in the quickstart is fully functional and production ready, but you may want to add more nodes for redundancy.
    -Try the Blog search and recommendation tutorial to learn more about using Vespa
    -See developing applications on adding your own Java components to your Vespa application.
    -Vespa APIs is useful to understand how to interface with Vespa
    -Explore the sample applications



## Deployment

    1 mvn package

    2 heroku deploy:war --war target/roadblock-1.0-SNAPSHOT.war

## Инструменты сборки

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Благотворительность

Пожалуйста ознакомьтесь [CONTRIBUTING.md](https://gitlab.rebrainme.com/anubis00786/rebrain-devops-task-checkout/blob/7375be600d2a127c7a7816f9272706ffb12ed664/CONTRIBUTING.md) хочется получить немного ваших денег.

## Версионность

Мы используем [SemVer](http://semver.org/) для назначени версий. 

## Авторы

* **Балакин Иван** - *Initial work* - [Где все началось](https://gitlab.rebrainme.com/anubis00786/rebrain-devops-task1)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Знания

* Если дернуть кота за хвост он обидится.
* Цветы не могут есть колбасу
* Приложение если и работает то это подозрительно .

