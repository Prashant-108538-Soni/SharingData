import 'package:flutter/material.dart';
import 'package:flutter_svg/svg.dart';

/// A customizable menu button with a dropdown of selectable options.
/// 
/// Displays a bordered button containing an SVG icon, which opens a popup menu
/// on tap. Menu items are passed as a list of strings, and the selected item
/// is returned via the [onSelect] callback.
class MenuButton extends StatelessWidget {
  /// List of menu option labels.
  final List<String> options;

  /// Callback triggered with the selected option.
  final ValueChanged<String> onSelect;

  /// Path to the SVG icon used in the button.
  final String iconPath;

  const MenuButton({
    super.key,
    required this.options,
    required this.onSelect,
    required this.iconPath,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
      decoration: BoxDecoration(
        border: Border.all(color: Theme.of(context).primaryColor),
        borderRadius: BorderRadius.circular(8),
      ),
      child: PopupMenuButton<String>(
        onSelected: onSelect,
        itemBuilder: (BuildContext context) => options
            .map((choice) => PopupMenuItem<String>(
                  value: choice,
                  child: Text(choice),
                ))
            .toList(),
        icon: SvgPicture.asset(
          iconPath,
          placeholderBuilder: (_) =>
              const Icon(Icons.error_outline, color: Colors.red),
        ),
        color: Colors.white,
        padding: EdgeInsets.zero,
        offset: const Offset(0, 42), // Position dropdown below the button
      ),
    );
  }
}