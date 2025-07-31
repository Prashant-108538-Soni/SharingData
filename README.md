import 'package:flutter/material.dart';

/// A reusable primary button styled according to the app's theme.
///
/// Displays a filled button using the theme’s `colorScheme.primary` color.
/// Optionally supports an icon placed before the label text.
/// Commonly used for high-emphasis actions across the app.
class PrimaryButton extends StatelessWidget {
  /// Text label displayed inside the button.
  final String title;

  /// Callback executed when the button is pressed.
  final VoidCallback onTap;

  /// Optional icon displayed before the text.
  final Widget? icon;

  const PrimaryButton({
    super.key,
    required this.title,
    required this.onTap,
    this.icon,
  });

  @override
  Widget build(BuildContext context) {
    final TextStyle? buttonTextStyle = Theme.of(context).textTheme.labelLarge;

    return ElevatedButton(
      onPressed: onTap,
      style: ElevatedButton.styleFrom(
        backgroundColor: Theme.of(context).colorScheme.primary,
        foregroundColor: Theme.of(context).colorScheme.onPrimary,
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8.0)),
      ),
      child: icon == null
          ? Text(
              title,
              style: buttonTextStyle?.copyWith(
                color: Theme.of(context).colorScheme.onPrimary,
                fontWeight: FontWeight.bold,
              ),
            )
          : Row(
              mainAxisSize: MainAxisSize.min,
              children: [
                icon!,
                const SizedBox(width: 8.0),
                Text(
                  title,
                  style: buttonTextStyle?.copyWith(
                    color: Theme.of(context).colorScheme.onPrimary,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ],
            ),
    );
  }
}