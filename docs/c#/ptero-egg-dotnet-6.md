# Egg Pterodactyl dotnet 6

```json
{
    "_comment": "DO NOT EDIT: FILE GENERATED AUTOMATICALLY BY PTERODACTYL PANEL - PTERODACTYL.IO",
    "meta": {
        "version": "PTDL_v2",
        "update_url": null
    },
    "exported_at": "2022-08-14T23:14:01+02:00",
    "name": "Discord.NET",
    "author": "raouf@ecipium.xyz",
    "description": null,
    "features": null,
    "docker_images": {
        "quay.io\/parkervcp\/pterodactyl-images:ubuntu_source": "quay.io\/parkervcp\/pterodactyl-images:ubuntu_source"
    },
    "file_denylist": [],
    "startup": "if [ ! -d \".\/.dotnet\" ]; then wget https:\/\/dot.net\/v1\/dotnet-install.sh && bash .\/dotnet-install.sh -c Current --runtime dotnet; fi; .\/.dotnet\/dotnet {{DLL_FILE}}",
    "config": {
        "files": "{}",
        "startup": "{\r\n    \"done\": \"Ready\"\r\n}",
        "logs": "{}",
        "stop": "^C"
    },
    "scripts": {
        "installation": {
            "script": null,
            "container": "quay.io\/parkervcp\/pterodactyl-images:ubuntu_source",
            "entrypoint": "bash"
        }
    },
    "variables": [
        {
            "name": "DLL to run",
            "description": "",
            "env_variable": "DLL_FILE",
            "default_value": "Program.dll",
            "user_viewable": true,
            "user_editable": true,
            "rules": "required|string|max:20",
            "field_type": "text"
        }
    ]
}
```