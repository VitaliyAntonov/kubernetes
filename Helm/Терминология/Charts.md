
https://helm.sh/docs/topics/charts/


Helm использует формат упаковки, называемый _диаграммами_ . Диаграмма — это набор файлов, описывающих связанный набор ресурсов Kubernetes. Одна диаграмма может использоваться для развертывания чего-то простого, например модуля memcached, или чего-то сложного, например полного стека веб-приложений с HTTP-серверами, базами данных, кэшами и т. д.

Диаграммы создаются в виде файлов, размещенных в определенном дереве каталогов. Их можно упаковать в версионные архивы для развертывания.

Если вы хотите скачать и просмотреть файлы опубликованной диаграммы, не устанавливая ее, вы можете сделать это с помощью 

`helm pull chartrepo/chartname`.

В этом документе объясняется формат диаграмм и даются основные рекомендации по созданию диаграмм с помощью Helm.


## Структура файла диаграммы

Диаграмма организована как набор файлов внутри каталога. Имя каталога — это имя диаграммы (без информации о версии). Таким образом, диаграмма, описывающая WordPress, будет храниться в `wordpress/`каталоге.

Внутри этого каталога Helm будет ожидать соответствующую структуру:

```text
wordpress/
  Chart.yaml          # A YAML file containing information about the chart
  LICENSE             # OPTIONAL: A plain text file containing the license for the chart
  README.md           # OPTIONAL: A human-readable README file
  values.yaml         # The default configuration values for this chart
  values.schema.json  # OPTIONAL: A JSON Schema for imposing a structure on the values.yaml file
  charts/             # A directory containing any charts upon which this chart depends.
  crds/               # Custom Resource Definitions
  templates/          # A directory of templates that, when combined with values,
                      # will generate valid Kubernetes manifest files.
  templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes
```


Helm оставляет за собой право использовать каталоги `charts/`, `crds/`, и `templates/`, а также перечисленные имена файлов. Остальные файлы останутся как есть.


## Файл Chart.yaml

Файл `Chart.yaml`необходим для диаграммы. Он содержит следующие поля:

```yaml
apiVersion: The chart API version (required)
name: The name of the chart (required)
version: A SemVer 2 version (required)
kubeVersion: A SemVer range of compatible Kubernetes versions (optional)
description: A single-sentence description of this project (optional)
type: The type of the chart (optional)
keywords:
  - A list of keywords about this project (optional)
home: The URL of this projects home page (optional)
sources:
  - A list of URLs to source code for this project (optional)
dependencies: # A list of the chart requirements (optional)
  - name: The name of the chart (nginx)
    version: The version of the chart ("1.2.3")
    repository: (optional) The repository URL ("https://example.com/charts") or alias ("@repo-name")
    condition: (optional) A yaml path that resolves to a boolean, used for enabling/disabling charts (e.g. subchart1.enabled )
    tags: # (optional)
      - Tags can be used to group charts for enabling/disabling together
    import-values: # (optional)
      - ImportValues holds the mapping of source values to parent key to be imported. Each item can be a string or pair of child/parent sublist items.
    alias: (optional) Alias to be used for the chart. Useful when you have to add the same chart multiple times
maintainers: # (optional)
  - name: The maintainers name (required for each maintainer)
    email: The maintainers email (optional for each maintainer)
    url: A URL for the maintainer (optional for each maintainer)
icon: A URL to an SVG or PNG image to be used as an icon (optional).
appVersion: The version of the app that this contains (optional). Needn't be SemVer. Quotes recommended.
deprecated: Whether this chart is deprecated (optional, boolean)
annotations:
  example: A list of annotations keyed by name (optional).
```

Начиная с [версии 3.3.2](https://github.com/helm/helm/releases/tag/v3.3.2) дополнительные поля не допускаются. Рекомендуемый подход — добавить пользовательские метаданные в файлы `annotations`.

### Диаграммы и версии

Каждая диаграмма должна иметь номер версии. Версия должна соответствовать стандарту [SemVer 2](https://semver.org/spec/v2.0.0.html) . В отличие от Helm Classic, Helm v2 и более поздние версии используют номера версий в качестве маркеров выпуска. Пакеты в репозиториях идентифицируются по имени и версии.

Например, `nginx`диаграмма, для которой установлено поле версии, `version: 1.2.3` будет называться:

```text
nginx-1.2.3.tgz
```

Также поддерживаются более сложные имена SemVer 2, такие как `version: 1.2.3-alpha.1+ef365`. Но имена, отличные от SemVer, явно запрещены системой.

**ПРИМЕЧАНИЕ.** В то время как Helm Classic и Deployment Manager были очень ориентированы на GitHub, когда дело доходило до диаграмм, Helm v2 и более поздние версии не полагаются на GitHub или даже Git и не требуют их. Следовательно, он вообще не использует Git SHA для управления версиями.

Поле `version`внутри `Chart.yaml`используется многими инструментами Helm, включая интерфейс командной строки. При создании пакета `helm package`команда будет использовать версию, найденную в `Chart.yaml`качестве токена в имени пакета. Система предполагает, что номер версии в имени пакета диаграмм совпадает с номером версии в файле `Chart.yaml`. Несоблюдение этого предположения приведет к ошибке.









