# Rake for 
### / ImageMagick Source Installer /
### / Creating & installation Vips lib /

## Требования

- **Ruby** (версия 2.5 и выше)
- **Rake**: `gem install rake`

# Установка
```bash
  git clone https://github.com/DRY9p/rake_install_imgck
```
# Использование

## Для установки
```bash
  rake imgck_install
```
```bash
  rake libvips_install
```

## Для удаления после установки
```bash
  rake rm_imgck
```

## Устновка solidus
### Example
```bash
  rake solidus_install ruby_v rails_v name

  rake solidus_install 3.3.7 7.2.2.1 example_store
```
